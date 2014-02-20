import processing.video.*;
PImage floorimage;

Capture video;

void setup() {
size(screen.width, screen.height, P3D);
// Uses the default video input, see the reference if this causes an error
video = new Capture(this, width, height, 10);
floorimage = loadImage ("floor.jpg");
noStroke();
smooth();
}

void draw() {
if (video.available()) {
video.read();
// Display the video (or not)
// image(video, 0, 0, width, height);
int darkestX = 0; // X-coordinate of the darkest video pixel
int darkestY = 0; // Y-coordinate of the darkest video pixel
float darkestValue = 255; // Brightness of the darkest video pixel
// Search for the darkest pixel: For each row of pixels in the video image and
// for each pixel in the yth row, compute each pixel's index in the video
video.loadPixels();
int index = 0;
for (int y = 0; y < video.height; y++) {
for (int x = 0; x < video.width; x++) {
// Get the color stored in the pixel
int pixelValue = video.pixels[index];
// Determine the brightness of the pixel
float pixelBrightness = brightness(pixelValue);
// If that value is brighter than any previous, then store the
// brightness of that pixel, as well as its (x,y) location
if (pixelBrightness < darkestValue) {
darkestValue = pixelBrightness;
darkestY = y;
darkestX = x;
}
index++;
}
}

// Floor projection
background(0);
noStroke();
fill(255,200);
ellipse(darkestX, darkestY, 200, 200);//draw an ellipse to tell me where the darkest point is

for (int y = 0; y < height; y+=90) {
for (int x = 0; x < width; x+=90) {
pushMatrix();
float a = dist(x,y,darkestX,darkestY);
tint (200,a);
float d = dist(x,y,darkestX,darkestY);

translate(x,y,d);
image (floorimage, 0,0,120,90);

popMatrix();
}
}
}
}
