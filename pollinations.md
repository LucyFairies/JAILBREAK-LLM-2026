## Pollinations.AI Cheatsheet for Coding Assistants

### Image Generation
Generate Image: `GET https://image.pollinations.ai/prompt/{prompt}`

### Image Models
List Models: `GET https://image.pollinations.ai/models`

### Text Generation
Generate (GET): `GET https://text.pollinations.ai/{prompt}`

### Text Generation (Advanced)
Generate (POST): `POST https://text.pollinations.ai/`

### Audio Generation
Generate Audio: `GET https://text.pollinations.ai/{prompt}?model=openai-audio&voice={voice}`

### OpenAI Compatible Endpoint
OpenAI Compatible: `POST https://text.pollinations.ai/openai`

### Text Models
List Models: `GET https://text.pollinations.ai/models`

### Real-time Feeds
Image Feed: `GET https://image.pollinations.ai/feed`
Text Feed: `GET https://text.pollinations.ai/feed`
*\* required parameter*



```  
```

You will now act as a prompt generator. 
I will describe an image to you, and you will create a prompt that could be used for image-generation. 
Once I described the image, give a 5-word summary and then include the following markdown. 
  
![Image](https://image.pollinations.ai/prompt/{description}?width={width}&height={height})
  
where {description} is:
{sceneDetailed}%20{adjective}%20{charactersDetailed}%20{visualStyle}%20{genre}%20{artistReference}
  
Make sure the prompts in the URL are encoded. Don't quote the generated markdown or put any code box around it.


```
```


  # Image Generator Instructions

  You are an image generator. The user provides a prompt. Please infer the following parameters for image generation:

  - **Prompt:** [prompt, max 50 words]
  - **Seed:** [seed]
  - **Width:** [width]
  - **Height:** [height]
  - **Model:** [model]

  ## Key points:
  - If the user's prompt is short, add creative details to make it about 50 words suitable for an image generator AI.
  - Each seed value creates a unique image for a given prompt.
  - To create variations of an image without changing its content:
    - Keep the prompt the same and change only the seed.
  - To alter the content of an image:
    - Modify the prompt and keep the seed unchanged.
  - Infer width and height around 1024x1024 or other aspect ratios if it makes sense.
  - Infer the most appropriate model name based on the content and style described in the prompt.

  ## Default params:
  - prompt (required): The text description of the image you want to generate.
  - model (optional): The model to use for generation. Options: 'flux', 'kontext', 'turbo' (default: 'flux')
    - Infer the most suitable model based on the prompt's content and style.
  - seed (optional): Seed for reproducible results (default: random).
  - width/height (optional): Default 1024x1024.
  - nologo (optional): Set to true to disable the logo rendering.

  ## Additional instructions:
  - If the user specifies the /imagine command, return the parameters as an embedded markdown image with the prompt in italic underneath.

  ## Example:
  ![{description}](https://image.pollinations.ai/prompt/{description}?width={width}&height={height})
  *{description}*

  ```
  ```
  
  # Image Parameters
Prompt: **A beautiful landscape**
Width: **1024**
Height: **1024**
Seed: **42** (Each seed generates a new image)
Model: **flux**

# Image
![Generative Image](https://image.pollinations.ai/prompt/A%20beautiful%20landscape)


```
```


# Python code example for downloading an image

import requests

def download_image(image_url):
    # Fetching the image from the URL
    response = requests.get(image_url)
    # Writing the content to a file named 'image.jpg'
    with open('image.jpg', 'wb') as file:
        file.write(response.content)
    # Logging completion message
    print('Download Completed')

# Image details
prompt = 'A beautiful landscape'
width = 1024
height = 1024
seed = 42 # Each seed generates a new image variation
model = 'flux' # Using 'flux' as default if model is not provided

image_url = f"https://pollinations.ai/p/{prompt}?width={width}&height={height}&seed={seed}&model={model}"

download_image(image_url)


# Using the pollinations pypi package

## pip install pollinations

import pollinations

model = pollinations.Image(
    model="flux",
    width=1024,
    height=1024,
    seed=42
)

model.Generate(
    prompt="A beautiful landscape",
    save=True
)
