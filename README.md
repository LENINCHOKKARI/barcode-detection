# barcode-detection
!pip install opencv-python-headless
!pip install pyzbar

# Install the ZBar library using apt
!apt install libzbar0
import cv2
from pyzbar.pyzbar import decode
from google.colab import files
from google.colab.patches import cv2_imshow

# Install necessary libraries
!pip install opencv-python-headless
!pip install pyzbar

# Install the ZBar library using apt
!apt install libzbar0

def detect_barcodes(image_path):
    # Load the image using OpenCV
    image = cv2.imread(image_path)
    
    # Convert the image to grayscale
    gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
    
    # Detect barcodes in the grayscale image
    barcodes = decode(gray)
    
    if barcodes:
        for barcode in barcodes:
            # Extract barcode data and type
            barcode_data = barcode.data.decode('utf-8')
            barcode_type = barcode.type
            
            # Draw a rectangle around the barcode on the original image
            x, y, w, h = barcode.rect
            cv2.rectangle(image, (x, y), (x + w, y + h), (0, 255, 0), 2)
            
            # Display barcode data and type
            print(f"Detected Barcode Type: {barcode_type}, Data: {barcode_data}")
    
    else:
        print("No barcodes detected in the image.")
    
    # Display the image with detected barcodes
    cv2_imshow(image)

# Upload an image containing a barcode
uploaded = files.upload()

# Assuming you uploaded an image named 'barcode_image.jpg'
image_path = 'barcode_image.jpg'

# Call the detect_barcodes function
detect_barcodes(image_path)
