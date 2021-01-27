# Optical_Mark_Recognition
Optical Mark Recognition in OMR sheets.

## Introduction:

Optical Mark Recognition, or OMR for short, is the process
of automaticallyanalyzing human- marked documents and
interpreting their results. Commonly used application of OMR is the
bubbled answer sheets for MCQs.
So, in this project, we are going to see how OMR is done on
bubbled sheets using PYTHON.

# Procedure:

• Firstly, let’s consider an
image that needs to be
processed. The image
that I am using is a
custom OMR sheet
(courtesy: Internet) for 5
questions with 5 options
each.

• After reading the
image, we have to
convert it to grayscale
for easier processing.

• Convolve the
grayscale image with
gaussian blur filter of size
(5,5) to remove impulse
noises like salt and
pepper noise.

• Now, pass the 2 dimensional gray image into Canny edge
detector.

• The output of Canny
edge detector is given:

• Next step is to find out where the
omr sheet is in the image.

• For this we make use of
OpenCV’s 'findContours'
function. We find all contours in
the image, arrange them in
descending order based on their
area.

• And consider the contour which
has four vertices.
(This is assuming the omr sheet is the
focus of the image and the omr
sheet is rectangular in shape)

• We crop out the region of interest
i.e. the omr sheet.

• We now start the actual process of
mark recognition.

• For this, we first convert the above
image into a binary image i.e.
containing only black and white.
This process is called thresholding.

• We use Otsu’s binarization which
sets the threshold value
automatically.

• This is the step where we identify the bubbles.

• Find the contours again and find each of their aspect ratio
( width / height).

• Since we know we are identifying circles, we also know the aspect
ratio is close to one.

• We also set a minimum size to rule out small circles.

• These 2 beforementioned conditions are applied to identify the
answer bubbles.

• All the selected contours are arranged in ascending order(left to
right and top to bottom).

• We start the marks calculation process.

• Since there are 5 options to each questions, we loop over 5
contours at once.

• To determine which bubble is marked, we make use of
cv2.countNonZero() function. This function gives the number of
pixels that have a non-zero value(255 here).

• We could take the bubble with maximum nonzero pixels as the
marked bubble, but we can see option naming inside the bubbles,
they can be considered as marked if the user hasn’t marked
anything.

• To avoid this case, we set a non-zero value threshold to be
considered as marked.

• If the user has marked more than 2 options, only the first one will be
considered.

• The question number
and option number is
being kept track of
while looping over the
contours. The option
number of the ‘marked
bubble’ that is detected
is tallied with the answer
key and the
percentage is
calculated.

The final output looks as
follows:

# Conclusion and Future Scope:
• We have successfully graded the OMR sheet using just Digital Image
Processing. But the solution that’s proposed is not well generalized.
The minimum size of bubbles and minimum number of non zero
values inside the bubble that are used in the process are all
constants specific to the given set of images.

• So, we can work on a more generalized solution that works with any
given OMR sheet.

