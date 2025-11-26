This notebook solves the problem posed by: https://github.com/achntrl/reorder-frames

The corrupted video has been shuffled and has some unrelated frames added to it. The goal is to remove the wrong frames and reorder the video.

The solution here works by tracking objects across frames (using RT-DETRv2 by Baidu, cf. https://arxiv.org/abs/2407.17140), removing frames where no object is detected, and then computing similarities between frames (in terms of a weighted sum of grayscale histogram distance and main bounding box tracking).

Using this similarity metric, the algorithm then finds a path of maximization of total similarity between adjactent frames (or a path of least total distance between frames), starting from candidates frames that are the most distant on average from the other frames. After that, a coherence check removes the frames that are not coherent with their neighbours in terms of tracked objects.
