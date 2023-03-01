# Lane-Detection-Open-CV
Using Hough Transform, detecting of the edges on the road and the lane
This code reads frames from a video file and detects lane lines in each frame using computer vision techniques. Here is a breakdown of the main parts of the code:

while True: creates an infinite loop that continues until the user presses the "Esc" key.
ret, or_frame = video.read() reads a frame from the video file and returns a flag ret indicating whether the frame was successfully read, and the actual frame or_frame.
if not ret: checks if the frame was not read successfully, which can happen when the video reaches the end. If this is the case, the code resets the video capture object and continues to the next iteration of the loop.
frame = cv2.GaussianBlur(or_frame, (5, 5), 0) blurs the image to reduce noise and make it easier to detect edges.
hsv = cv2.cvtColor(frame, cv2.COLOR_BGR2HSV) converts the blurred image from the default color space (BGR) to the HSV color space, which is more suitable for detecting yellow and white lane lines.
lower_y = np.array([18, 94, 140]) and upper_y = np.array([18, 255, 255]) define the lower and upper boundaries of the yellow color in the HSV color space, respectively.
mask = cv2.inRange(hsv, lower_y, upper_y) creates a binary image mask that only shows pixels within the yellow color range.
edges = cv2.Canny(mask, 74, 150) applies the Canny edge detection algorithm to the masked image to extract the edges of the lane lines.
lines = cv2.HoughLinesP(edges, 1, np.pi / 180, 50, maxLineGap=50) applies the probabilistic Hough transform to the edge image to detect straight line segments, which represent the lane lines. The maxLineGap parameter controls the maximum gap between line segments that can be merged into a single line.
if lines is not None: checks if any lines were detected in the image. If so, the code iterates over each line and draws it on the original frame using cv2.line.
cv2.imshow("frame", frame) displays the original frame with the detected lane lines overlaid on it.
cv2.imshow("edges", edges) displays the edge image.
key = cv2.waitKey(25) waits for a key press for 25 milliseconds before proceeding to the next iteration of the loop.
if key == 27: checks if the pressed key is the "Esc" key (with ASCII value 27). If so, the code breaks out of the loop and terminates the program.
