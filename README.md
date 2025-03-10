# aafrom PIL import Image
import sys

# Define ASCII characters from dark to light
ASCII_CHARS = "@%#*+=-:. "

def resize_image(image, new_width=100):
    width, height = image.size
    aspect_ratio = height / width
    new_height = int(new_width * aspect_ratio * 0.55)  # Adjusting aspect ratio
    return image.resize((new_width, new_height))

def grayscale(image):
    return image.convert("L")

def pixels_to_ascii(image):
    pixels = image.getdata()
    ascii_str = "".join(ASCII_CHARS[pixel // 32] for pixel in pixels)  # Scale pixels to ASCII_CHARS
    return ascii_str

def image_to_ascii(image_path, new_width=100):
    try:
        image = Image.open(image_path)
    except Exception as e:
        print(f"Unable to open image: {e}")
        return
    
    image = resize_image(image, new_width)
    image = graysc