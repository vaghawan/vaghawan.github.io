## Training YoloV2 in Custom Dataset

Without sounding too smart as if to understand every tip of the YOLO artitecture, in this article I would rather show you a lame approach of plugging the custom data set and training a new model in the Google open image datasets. 

#Data Sets: I’m using the dataset provided by [google open image](https://storage.googleapis.com/openimages/web/index.html) , the data looks quite like this: 

Show the gist here..

```
ImageID,Source,LabelName,Confidence,XMin,XMax,YMin,YMax,IsOccluded,IsTruncated,IsGroupOf,IsDepiction,IsInside,Class,x,y,width,height
078821d86db99fc9.jpg,freeform,/m/014j1m,1,0.244277,0.542485,0.09314,0.539359,1,0,0,0,0,Apple,0.393381,0.3162495,0.29820800000000003,0.44621900000000003
078821d86db99fc9.jpg,freeform,/m/014j1m,1,0.383319,0.6979920000000001,0.474829,0.9430149999999999,1,0,0,0,0,Apple,0.5406555000000001,0.7089219999999998,0.31467300000000004,0.46818599999999994
09a06df60e4bdd62.jpg,freeform,/m/014j1m,1,0.0,0.999692,0.0,0.9931639999999999,0,0,1,0,0,Apple,0.499846,0.49658199999999997,0.999692,0.9931639999999999
0fdea8a716155a8e.jpg,freeform,/m/014j1m,1,0.013999999999999999,0.991891,0.0,0.985716,0,0,1,0,0,Apple,0.5029454999999999,0.492858,0.977891,0.985716
105433f9d808d18e.jpg,freeform,/m/014j1m,1,0.12879300000000002,0.8589479999999999,0.102363,0.854827,0,0,0,0,0,Apple,0.4938705,0.478595,0.7301549999999999,0.752464


```

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

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