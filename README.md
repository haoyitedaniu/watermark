# watermark

This is my attempt at a LSB Steganographic watermarking implementation in Javascript. Slightly hacky demo, use at your own risk.

This is a simple watermarking app that applies a watermark image to a target image. The watermark cannot be seen, but it can be extracted later using the extract method in the app - in other words, it hides one image inside another. I have used a tiny NodeJS/Express server to get around CORS errors that arise from messing with images in a canvas, so use npm start and load http://localhost:8080/watermark.htm in your browser to run it. 
        
- load pics - loads 2 images

- watermark - creates a watermarked image (image A hidden in image B)

- extract - pulls the watermark out and displays it
  
    
## How it works:

-Image A is the watermark; Image B is the image to be watermarked.
        
- A is compressed from 32bit (RGBA) into 2 bits per channel by dividing each color channel value by 65 and applying bitwise OR 0x03. This reduces the range 0-255 to 0-3, which fits into 2 bits.
        
- These 2 bits per pixel then overwrite the least-significant 2 bits of the channels in the target image to be watermarked.  
        
- The watermark is extracted by taking the 2 LSBs (bitwise AND 0xFC) and multiplying by 65 to re-hydrate the watermark into an approximation of the original image.

The watermark is invisible to the naked eye. Extracted watermarks are color, and look pretty good.


