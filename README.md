# encryption-image
Here's a simple image encryption tool using Python and the Pillow library. This code swaps pixel values and applies a basic mathematical operation to each pixel.

```
from PIL import Image

def encrypt_image(image_path, key):
    """
    Encrypts an image by swapping pixel values and applying a mathematical operation.
    
    Args:
    image_path (str): Path to the image file.
    key (int): Encryption key.
    
    Returns:
    encrypted_image: Encrypted image object.
    """
    image = Image.open(image_path)
    pixels = image.load()
    width, height = image.size
    
    encrypted_image = Image.new(image.mode, image.size)
    encrypted_pixels = encrypted_image.load()
    
    for x in range(width):
        for y in range(height):
            pixel = pixels[x, y]
            # Apply a simple mathematical operation (e.g., XOR) to each pixel value
            encrypted_pixel = tuple((p ^ key) for p in pixel)
            encrypted_pixels[x, y] = encrypted_pixel
    
    return encrypted_image

def decrypt_image(encrypted_image, key):
    """
    Decrypts an image by reversing the encryption operation.
    
    Args:
    encrypted_image: Encrypted image object.
    key (int): Encryption key.
    
    Returns:
    decrypted_image: Decrypted image object.
    """
    pixels = encrypted_image.load()
    width, height = encrypted_image.size
    
    decrypted_image = Image.new(encrypted_image.mode, encrypted_image.size)
    decrypted_pixels = decrypted_image.load()
    
    for x in range(width):
        for y in range(height):
            pixel = pixels[x, y]
            # Reverse the XOR operation to decrypt the pixel values
            decrypted_pixel = tuple((p ^ key) for p in pixel)
            decrypted_pixels[x, y] = decrypted_pixel
    
    return decrypted_image

def main():
    image_path = input("Enter the image file path: ")
    key = int(input("Enter the encryption key: "))
    
    encrypted_image = encrypt_image(image_path, key)
    encrypted_image.save("encrypted_image.png")
    print("Encrypted image saved as encrypted_image.png")
    
    decrypted_image = decrypt_image(encrypted_image, key)
    decrypted_image.save("decrypted_image.png")
    print("Decrypted image saved as decrypted_image.png")

if _name_ == "_main_":
    main()
