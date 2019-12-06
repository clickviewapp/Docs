# ClickView Image API

The ClickView Image API is used to obtain the images used in various ClickView resources.

## Resource URL
```http
GET https://img.clickviewapp.com/v2/{imageType}/{imageId}
```
 
## Path Parameters
| Parameter | Required | Description | Example |
| --------- | -------- |------------ | ------- |
| imageType | required | The type of image. See [here](image_types.md) for a list of types | `thumbnails` |
| imageId | required | The image ID | `X5ramO` |

## Query Parameters

| Parameter | Required | Description | Example |
| --------- | -------- |------------ | ------- |
| width | optional | The width of the image in pixels | `1920` |
| height | optional | The height of the image in pixels | `1080` |
| size | optional | Presets for the width and height. See [here](image_types.md) for a list of sizes | `small` |
| ratio | optional | The ratio to lock the image to if either the width or height is left empty | `16:9` | 
| resizeType | optional | The resize method to use when the desired aspect ratio doesn't match the original aspect ratio. See [here](resize_types.md) for a list of resize types | `cover` |
| bgColor | optional | The hex color of the padding (ignored if a `resizeType` other than `crop` is used) | `f8981d` |
| imageQuality | optional | The image quality as a value from `0-100` | `90` |

## Examples

> https://img.clickviewapp.com/v2/thumbnails/X5ramO?size=medium   
> Returns a medium-size thumbnail

> https://img.clickviewapp.com/v2/thumbnails/X5ramO?size=small?imageQuality=30  
> Returns a small thumbnail with an image quality of 30  

> https://img.clickviewapp.com/v2/thumbnails/X5ramO?width=800&height=300&bgColor=f8981d  
> Returns a thumbnail with a width of 800, height of 300 and orange borders   

> https://img.clickviewapp.com/v2/thumbnails/X5ramO?width=800&height=300&resizeType=stretched  
> Returns a thumbnail with a width of 800, height of 300, stretched to fill the specified dimensions

> https://img.clickviewapp.com/v2/thumbnails/X5ramO?width=800&ratio=2:1  
> Returns a thumbnail with a width of 800 and aspect ratio of 2:1   