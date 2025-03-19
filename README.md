# Wolf-s-suppository-
Oops repository 
import os
from PIL import Image

def mass_import_images(directory, extensions=(".jpg", ".jpeg", ".png", ".gif")):
    """
    Imports images from a specified directory.

    Args:
        directory (str): The path to the directory containing the images.
        extensions (tuple, optional): A tuple of image file extensions to include.
                                      Defaults to (".jpg", ".jpeg", ".png", ".gif").

    Returns:
        dict: A dictionary where keys are image file paths and values are PIL Image objects.
              Returns an empty dictionary if no images are found or an error occurs.
    """
    images = {}
    try:
        for filename in os.listdir(directory):
            if filename.lower().endswith(extensions):
                filepath = os.path.join(directory, filename)
                try:
                    img = Image.open(filepath)
                    images[filepath] = img
                except (IOError, OSError) as e:
                    print(f"Error opening image: {filepath} - {e}")

    except FileNotFoundError:
        print(f"Directory not found: {directory}")

    return images

# Example usage:
image_directory = "path/to/your/images"  # Replace with your directory path
imported_images = mass_import_images(image_directory)

if imported_images:
    print(f"Imported {len(imported_images)} images.")
    # Example: Accessing and displaying the first image
    first_filepath = list(imported_images.keys())[0]
    first_image = imported_images[first_filepath]
    #first_image.show() # uncomment to display the first image. Note: show() may not work in all environments.
