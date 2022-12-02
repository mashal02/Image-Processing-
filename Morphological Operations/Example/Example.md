![pic](https://user-images.githubusercontent.com/83532882/205194296-ced3b646-fa4a-4a66-95d5-768301320c97.jpg)

To remove the extra colored lines, we perform thresholding. And to fill the gaps in the text, we perform other operations like closing and dilation. 

Python code:
#organizing imports
import cv2
import numpy as np

#path to input image is specified and
#image is loaded with imread command
image1 = cv2.imread('pic.jpg')


#to convert the image in grayscale
img = cv2.cvtColor(image1, cv2.COLOR_BGR2GRAY)


#all pixels value above 31 will
#be set to 255
ret, thresh1 = cv2.threshold(img, 31, 255, cv2.THRESH_BINARY)

#inverting the image
invert = cv2.bitwise_not(thresh1)

#define the kernel
kernel = np.ones((8, 8), np.uint8)
 
#closing the image
closing = cv2.morphologyEx(invert, cv2.MORPH_CLOSE, kernel, iterations=1)

#dilating
kernel = np.ones((3, 3), np.uint8)
dil = cv2.dilate(closing, kernel,
                   iterations=1)

#dilating again but with different kernel
kernel = np.ones((2, 2), np.uint8)
dil2 = cv2.dilate(dil, kernel,iterations=2)

#opening again with different kernel
kernel = np.ones((5, 5), np.uint8)
closing = cv2.morphologyEx(dil2, cv2.MORPH_CLOSE, kernel, iterations=1)

#inverting the image
invert = cv2.bitwise_not(closing)
cv2.imwrite("neww.jpg",invert) 


#De-allocate any associated memory usage
if cv2.waitKey(0) & 0xff == 27:
	cv2.destroyAllWindows()
  
  
Output:

![neww](https://user-images.githubusercontent.com/83532882/205195689-326dd0e7-b60f-4293-98ac-ee2162b650ca.jpg)

