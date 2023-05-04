# Image Steganography using Java

This is a documentation for embedding and decoding messages in images using Java. It uses image steganography, a technique of hiding data within an image without being noticed. 

## Embedding and Decoding Messages

### Requirements

To run this program, you need:

- Java Development Kit (JDK)
- Java Integrated Development Environment (IDE)

### Usage

1. Clone the repository or download the code files. 
2. Open the code in a Java IDE. 
3. Compile and run the `EmbedMessage.java` or `DecodeMessage.java` file depending on whether you want to embed or decode a message.
4. For embedding: 
   1. Click the `Open` button to select an image file in which you want to embed the message. 
   2. Enter the message you want to hide in the `Message to be embedded` text area. 
   3. Click the `Embed` button to embed the message in the image. 
   4. The steganographed image will be displayed in the `Steganographed Image` pane. 
   5. Click the `Save into new file` button to save the steganographed image as a new file. 
   6. Click the `Reset` button to start over with a new image. 

   For decoding: 
   1. Click the `Open` button to select the steganographed image file from which you want to extract the hidden message. 
   2. Click the `Decode` button to extract the hidden message from the image. 
   3. The hidden message will be displayed in the `Message` text area. 
   4. Click the `Reset` button to start over with a new image.

### Libraries

This program uses the following Java libraries:

- `java.awt.image.*`
- `javax.swing.*`
- `java.awt.*`
- `java.awt.event.*`
- `javax.imageio.*`

### Variables

- `open`: a `JButton` to open an image file or a steganographed image file. 
- `embed`: a `JButton` to embed the message in the image.
- `decode`: a `JButton` to decode the hidden message from the image. 
- `save`: a `JButton` to save the steganographed image as a new file. 
- `reset`: a `JButton` to reset the interface to its initial state. 
- `message`: a `JTextArea` to enter or display the message to be embedded or extracted from the image.
- `sourceImage`: a `BufferedImage` object to store the original image.
- `embeddedImage`: a `BufferedImage` object to store the steganographed image. 
- `sp`: a `JSplitPane` object to divide the interface into two panes. 
- `originalPane`: a `JScrollPane` object to display the original image. 
- `embeddedPane`: a `JScrollPane` object to display the steganographed image.

### Methods

#### `assembleInterface()`

This method sets up the graphical user interface (GUI) with the necessary buttons and text areas.

#### `actionPerformed(ActionEvent event)`

This method listens for button clicks and calls the appropriate method based on the button clicked.

#### `showFileDialog(boolean open)`

This method displays a file chooser dialog for the user to select an image file or a steganographed image file.

#### `openImage(File file)`

This method reads in the selected image file or steganographed image file and displays it in the appropriate pane.

#### `embedMessage(BufferedImage img, String mess)`

This method embeds the message in the image by modifying the least significant bits of each pixel in the image to represent the bits of the message. The method takes in two parameters - the image in which the message needs to be embedded, and the message itself. The method first checks if the message can be embedded in the image by checking if the length of the message is less than the total number of pixels in the image multiplied by 3 (since each pixel has three color channels - red, green, and blue). If the message length exceeds this limit, an IllegalArgumentException is thrown.

The method then converts the message into a binary string and iterates through each pixel in the image. For each pixel, the method retrieves the red, green, and blue values of the pixel and modifies their least significant bits to represent the next three bits of the binary message. This is done by first converting the red, green, and blue values to binary and then modifying the least significant bits of these binary values to represent the message bits. The modified binary values are then converted back to integers and used to set the red, green, and blue values of the pixel. Once all the message bits have been embedded, the method returns the modified image.

extractMessage(BufferedImage img)
This method extracts the message from the image by retrieving the least significant bits of each pixel in the image and concatenating them to form the binary message. The method takes in one parameter - the image from which the message needs to be extracted. The method iterates through each pixel in the image and retrieves the least significant bits of the red, green, and blue values of the pixel. These bits are then concatenated to form the binary message. Once all the pixels have been processed, the binary message is converted back to a string and returned. If the message cannot be extracted from the image (e.g. if there was no message embedded in the image), the method returns an empty string.
The `decodeMessage()` method is used to extract the message from the steganographed image. It uses the `extractInteger(BufferedImage img, int start, int storageBit)` method to extract the length of the message from the first 32 bits of the image. It then extracts each byte of the message using the `extractByte(BufferedImage img, int start, int storageBit)` method and concatenates them to form the original message.

The `extractInteger(BufferedImage img, int start, int storageBit)` method extracts an integer value from the image starting from the `start` index and using the specified `storageBit` to extract the individual bits.

The `extractByte(BufferedImage img, int start, int storageBit)` method extracts a byte value from the image starting from the `start` index and using the specified `storageBit` to extract the individual bits.

The `getBitValue(int n, int location)` method is used to extract the value of the bit at the specified `location` in the binary representation of the integer `n`.

Overall, the `ImageSteganography` project consists of two Java classes, `EmbedMessage` and `DecodeMessage`, that provide a GUI-based solution for embedding and decoding messages in images using steganography. The `EmbedMessage` class provides a GUI interface for embedding a message in an image, while the `DecodeMessage` class provides a GUI interface for extracting the hidden message from a steganographed image. Both classes use similar methods for embedding and decoding messages and share a common set of libraries used for image manipulation in Java.
