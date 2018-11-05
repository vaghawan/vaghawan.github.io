## Training YoloV2 in Custom Dataset

Without sounding too smart as if to understand every tip of the YOLO artitecture, in this article I would rather show you a lame approach of plugging the custom data set and training a new model in the Google open image datasets. If you're however to curious to understand it, you could follow the author's [webpage](https://pjreddie.com/darknet/yolo/) and the [articles](https://pjreddie.com/publications/). 


#Data Sets: I’m using the dataset provided by [google open image](https://storage.googleapis.com/openimages/web/index.html) , the data looks quite like this: 

You can also find the sample file in the project repo. 

```
ImageID,Source,LabelName,Confidence,XMin,XMax,YMin,YMax,IsOccluded,IsTruncated,IsGroupOf,IsDepiction,IsInside,Class,x,y,width,height
078821d86db99fc9.jpg,freeform,/m/014j1m,1,0.244277,0.542485,0.09314,0.539359,1,0,0,0,0,Apple,0.393381,0.3162495,0.29820800000000003,0.44621900000000003
078821d86db99fc9.jpg,freeform,/m/014j1m,1,0.383319,0.6979920000000001,0.474829,0.9430149999999999,1,0,0,0,0,Apple,0.5406555000000001,0.7089219999999998,0.31467300000000004,0.46818599999999994
09a06df60e4bdd62.jpg,freeform,/m/014j1m,1,0.0,0.999692,0.0,0.9931639999999999,0,0,1,0,0,Apple,0.499846,0.49658199999999997,0.999692,0.9931639999999999
0fdea8a716155a8e.jpg,freeform,/m/014j1m,1,0.013999999999999999,0.991891,0.0,0.985716,0,0,1,0,0,Apple,0.5029454999999999,0.492858,0.977891,0.985716
105433f9d808d18e.jpg,freeform,/m/014j1m,1,0.12879300000000002,0.8589479999999999,0.102363,0.854827,0,0,0,0,0,Apple,0.4938705,0.478595,0.7301549999999999,0.752464


```

### Markdown

We downloaded the whole image dataset worth around 5.x gb using https://github.com/cvdfoundation/open-images-dataset#download-full-dataset-with-google-storage-transfer 

We have the two main csv files, one for training and validation. Our purpose is just to train a model which can detect 12 different fruits available in the google open image and create a bounding box on them. So, we will filter out our desired class from the main csv files and create a smaller csv which contains only those categories in which we’re interested.  


```
import pandas as pd
df = pd.read_csv('train_data_description.csv')
val_df = pd.read_csv('validation_all.csv')


"""This is the list of class we're intrested in"""
list_of_class = ["Apple", "Banana", "Orange", "Pear", "Mango","Pineapple", "Lemon", "Watermelon", "Strawberry",
                "Grapefruit", "Peach", "Pomegranate"]


def prepareData(dataframe:pd.DataFrame(), list_of_class:list) -> pd.DataFrame() : 
    
    '''Accepts a dataframe of either train or validate data, and split our desired classes from the original
    dataset, and create a new dataset for our pre-processing purposes.'''
    
    dff= dataframe[dataframe['Class'].isin(list_of_class)]
    data = dff.drop(dff.index)
    
    for cls in list_of_class:
        count = dff[dff["Class"]==cls]
        print("for class "+ cls ,count.shape)
        
        #We're only taking the 1000 annotation for each category to maintain the categorical dispersity in dataset. 
        data = data.append(dff[dff["Class"]==cls][:1000])
    
    data['ImageID'] = data['ImageID'].apply(lambda a: a+'.jpg')
    if "Unnamed: 0" in data:
        data.drop(columns=["Unnamed: 0"], inplace=True)
    return data


train = prepareData(df, list_of_class)
val = prepareData(val_df, list_of_class)
train.to_csv('train_fruits_1.csv', index=False)
val.to_csv('val_fruits_1.csv', index=False)

```

The above process is only necessary if you have the the training and validation csv downloaded from the google open image. If however you haven't I've uploaded the csv files concerning the data in the project repo. The two csv file contains the 1000 data point of each fruit category.


# Converting Annotation Bbox to Yolo Format

So with the train and validation csv generated from the above code, we shall now move on to making the data suitable for the yolo. Yolo doesn’t use the same annotation box as in object detection model like Faster-RCNN provided in tensorflow model zoo. Rather yolo needs `centerX`, `centerY`, `width` and `height`. 

So we have to convert the annotation, which basically is `Xmin`, `Xmax`, `Ymin`, `Ymax` from our new csvs to something like:

```
<class_number> (<absolute_x> / <image_width>) (<absolute_y> / <image_height>) (<absolute_width> / <image_width>) (<absolute_height> / <image_height>)

```

The following codes does the calculation and gives us the required values:

```
# The following code is the modified version of codes available here: 
# https://blog.goodaudience.com/part-1-preparing-data-before-training-yolo-v2-and-v3-deepfashion-dataset-3122cd7dd884

def convert_labels(path, x1, y1, x2, y2):
    """
    Definition: Parses label files to extract label and bounding box
        coordinates.  Converts (Xmin, Ymin, Xmax, Ymax) annotation format to
        (x, y, width, height) normalized YOLO format.
    """
    def sorting(l1, l2):
        if l1 > l2:
            lmax, lmin = l1, l2
            return lmax, lmin
        else:
            lmax, lmin = l2, l1
            return lmax, lmin
    
    size = get_img_shape(path)
    if(size[1]==None):
        print(path, "not found")
        return '', '', '', ''
    xmax, xmin = sorting(x1, x2)
    ymax, ymin = sorting(y1, y2)
    dw = 1./size[1]
    dh = 1./size[0]
    x = (x1 + x2)/2.0
    y = (y1 + y2)/2.0
    w = x2 - x1
    h = y2 - y1
    x = x*dw
    w = w*dw
    y = y*dh
    h = h*dh
    return (x/dw,y/dh,w/dw,h/dh)


def get_img_shape(path):
    path = path
    img = cv2.imread(path)
    try:
        return img.shape
    except AttributeError:
        print('error! ', path)
        return (None, None, None)

```
Let's append the new columns in the existing training and validation files which consists the annotation. 

```
train['x'], train['y'], train['width'], train['height'] = \
    zip(*train.progress_apply(lambda row: convert_labels("test_yolo/eval/"+row['ImageID'], row['XMin'], row['YMin'], row['XMax'], row['YMax']), axis=1)) # Like python for one lone code.

train.to_csv('test_yolo/fruits_1.csv', index=False)

val['x'], val['y'], val['width'], val['height'] = \
    zip(*val.progress_apply(lambda row: convert_labels("test_yolo/eval/"+row['ImageID'], row['XMin'], row['YMin'], row['XMax'], row['YMax']), axis=1)) # Like python for one lone code.

val.to_csv('test_yolo/fruits_val_1.csv', index=False)

```
# Let Us Now Test The Conversion: 

```
import matplotlib.pyplot as plt
def from_yolo_to_cor(box, shape):
    img_h, img_w, _ = shape
    im_w = 1./img_w
    im_h = 1./img_h
    #box = [b/1000 for b in box]
    # x1, y1 = ((x + witdth)/2)*img_width, ((y + height)/2)*img_height
    # x2, y2 = ((x - witdth)/2)*img_width, ((y - height)/2)*img_height
    x1, y1 = int((box[0] + box[2]/2)*img_w), int((box[1] + box[3]/2)*img_h)
    x2, y2 = int((box[0] - box[2]/2)*img_w), int((box[1] - box[3]/2)*img_h)
    return abs(x1), abs(y1), abs(x2), abs(y2)
    
def draw_boxes(img, boxes):
    shape = np.array([768, 1024, 3])
    for box in boxes:
        x1, y1, x2, y2 = from_yolo_to_cor(box, shape)
        print(x1, y1, x2, y2)
        cv2.rectangle(img, (x2, y2), (x1, y1), (0,255,0), 3)
        #cv2.rectangle(img, (int(0.311875*768), int(0.591597*768) ), (int(0.461875*1024),int(0.768908*1024)) ,(0,255,0), 3)
    plt.imshow(img)
    plt.plot()
    plt.show()
imgs = train[train["ImageID"]=="000d9c59687b509b.jpg"]
#This is the list of values associated with that image id. Here the code can be improved. 
boxes = [[0.189062,0.189584,0.378125,0.379167],[0.57625,0.622084,0.5925,0.485833],[0.36625,0.509583,0.03875,0.0525]]
#boxes = [[0.73, 0.507380073800738, 0.395, 0.5940959409594095]]
draw_boxes(cv2.imread("test_yolo/train/000d9c59687b509b.jpg"), boxes)

```
The output should look like this: 

![]({% static 'static/images/appletest.png' %})
![]({% static 'static/images/apple-test-original.png' %})

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/vaghawan/vaghawan.github.io/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.