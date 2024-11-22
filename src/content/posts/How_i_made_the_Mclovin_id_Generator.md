---
title: 🤓 How i made the Mclovin Style Id Generator
published: 2024-11-18
description: "If you're going to impersonate a 25-year-old organ donor from Hawaii, you better do it right. Let’s dive in and see how it all came together!"
tags: [Web Design]
category: Mclovin Site
draft: false
---

# Purpose of the code
 McLovin: The Only Name You’ll Ever Need

 Basically, it turns your dreams into reality... well, if your dream was to have an ID like McLovin’s, but with your own face. This code lets you upload your photo, making your ID truly one of a kind. Forget boring generic IDs—this is your moment to shine! Feel free to use it, improve it, or completely reinvent it. After all, if a 25-year-old Hawaiian organ donor can do it, so can you. Just hope you don’t get hit like McLovin did when you use it.

But hey, on the bright side, here’s to hoping you end up like the legend himself—getting laid and living the dream.

## "Officially Unofficial" ID
<img src="/favicon/mclovin_card.png" width="3100" height="2100" alt="Tarjeta de McLovin">

# Code explanation

This is the code that makes the ID generator come to life. In simple terms, it allows you to upload an image, resizes it, and places it perfectly in the photo spot on the ID. It's like magic—but with code!

### Full Code

```python
from flask import Flask, request, send_file, render_template
from PIL import Image
import io

app = Flask(__name__)

@app.route('/')
def index():
    return render_template('index.html')

@app.route('/generate_card', methods=['POST'])
def generate_card():
   
    base_image = Image.open('mclovin_template.png')  

    
    photo = request.files['photo']
    user_photo = Image.open(photo)

    
    width, height = user_photo.size
    min_dim = min(width, height)
    left = (width - min_dim) / 2
    top = (height - min_dim) / 2
    right = (width + min_dim) / 2
    bottom = (height + min_dim) / 2
    user_photo = user_photo.crop((left, top, right, bottom))

    
    user_photo = user_photo.resize((251, 278))  
    base_image.paste(user_photo, (8, 6))  

    
    img_io = io.BytesIO()
    base_image.save(img_io, 'PNG')
    img_io.seek(0)

    return send_file(img_io, mimetype='image/png', as_attachment=True, download_name='mclovin_card.png')

if __name__ == '__main__':
    app.run(debug=True)
```

## Step 1
### Importing Required Libraries

```python
from flask import Flask, request, send_file, render_template
from PIL import Image
import io
```
* Flask: Used to create the web application and handle HTTP requests.
* PIL (Pillow): Provides tools to manipulate images.
* io: Helps create in-memory file-like objects for image processing.

## Step 2
### Initializing the Flask Application


```python
app = Flask(__name__)
```
* Creates a Flask app instance for handling routes and requests.

## Step 3
### Defining Routes
#### Root Route

```python
@app.route('/')
def index():
    return render_template('index.html')
```
* This defines the homepage (route /).
* It serves the index.html file, which likely contains the UI for uploading a photo.

#### Generate Card Route

```python
@app.route('/generate_card', methods=['POST'])
def generate_card():
```
* This route handles the POST request sent when the user submits a photo.
* The main function logic for generating the fake McLovin ID is implemented here.

## Step 4
### Loading the Base Template


```python
base_image = Image.open('mclovin_template.png')
```
* Opens the base image (e.g., McLovin ID card template) to which the uploaded photo will be added.

## Step 5
### Handling the Uploaded Photo


```python
photo = request.files['photo']
user_photo = Image.open(photo)
```
* Receives the uploaded photo via the request.
* Opens the uploaded photo using Pillow.

## Step 6
### Cropping the Photo to a Square


```python
width, height = user_photo.size
min_dim = min(width, height)
left = (width - min_dim) / 2
top = (height - min_dim) / 2
right = (width + min_dim) / 2
bottom = (height + min_dim) / 2
user_photo = user_photo.crop((left, top, right, bottom))
```
* Extracts the smaller dimension (width or height) to crop the photo into a square.
* Calculates the coordinates for cropping the center portion of the image.
* Crops the image using the calculated coordinates. 

## Step 7
### Resizing the Photo


```python
user_photo = user_photo.resize((251, 278))
```
* Resizes the cropped photo to fit the placeholder dimensions on the ID template.

## Step 8
### Pasting the Photo onto the Template

```python
base_image.paste(user_photo, (8, 6))
```

* Pastes the resized photo onto the ID template at the specified position (x=8, y=6).
* You can use Photoshop or any other photo editing software to obtain the coordinates.

## Step 9
### Saving the Final ID

```python
img_io = io.BytesIO()
base_image.save(img_io, format='PNG')
img_io.seek(0)
```

* Saves the final ID card into an in-memory file-like object (img_io) in PNG format.
* Resets the file pointer to the beginning (seek(0)) to prepare it for downloading.

## Step 10
### Saving the Final ID

```python
return send_file(img_io, mimetype='image/png', as_attachment=True, download_name='mclovin_card.png')
```

* Sends the generated ID card to the user as a downloadable PNG file named mclovin_card.png.

## Step 11
### Running the Application

```python
if __name__ == '__main__':
    app.run(debug=True)
```

* Starts the Flask app in debug mode, enabling error messages and hot-reloading during development.


# 💬 Comments 
### "Thank you for reading! 😊 Feel free to leave a comment 💬 and share your reaction 👍—your thoughts are always welcome!"

<script id="giscus-script" src="https://giscus.app/client.js"
        data-repo="MauroQ80/Personal-Blog"
        data-repo-id="R_kgDONPH48A"
        data-category="General"
        data-category-id="DIC_kwDONPH48M4CkdQw"
        data-mapping="url"
        data-strict="0"
        data-reactions-enabled="1"
        data-emit-metadata="0"
        data-input-position="bottom"
        data-theme="dark_protanopia" 
        data-lang="en"
        crossorigin="anonymous"
        async>
</script>