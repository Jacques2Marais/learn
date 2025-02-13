# Chapter 4: Deep Learning

## Neural Networks Basics

Neural networks are the foundation of deep learning. They are inspired by the structure of the human brain and consist of interconnected nodes called neurons.

*   **Perceptron:** The basic building block of a neural network. It takes multiple inputs, applies weights and a bias, and then passes the result through an activation function to produce an output.
*   **Activation Functions:** Introduce non-linearity into the network, allowing it to learn complex patterns. Common activation functions include:
    *   **Sigmoid:** Outputs values between 0 and 1, useful for binary classification.
    *   **ReLU (Rectified Linear Unit):** Outputs 0 for negative inputs and the input value for positive inputs, computationally efficient.
    *   **Tanh (Hyperbolic Tangent):** Outputs values between -1 and 1, similar to sigmoid but centered around zero.
*   **Feedforward Networks:** The simplest type of neural network, where information flows in one direction from the input layer to the output layer through hidden layers.
*   **Backpropagation:** The algorithm used to train feedforward neural networks. It calculates the gradients of the loss function with respect to the network's weights and biases and uses these gradients to update the weights and biases in the direction that minimizes the loss.

## Convolutional Neural Networks (CNNs)

Convolutional Neural Networks (CNNs) are a specialized type of neural network designed for processing grid-like data, such as images.

*   **Architecture of CNNs:** CNNs typically consist of convolutional layers, pooling layers, and fully connected layers.
*   **Convolutional Layers:** The core building blocks of CNNs. They perform convolution operations on the input image using filters (kernels) to extract features.
    *   **Filters (Kernels):** Small matrices that slide over the input image, performing element-wise multiplication and summation to detect specific features (e.g., edges, corners).
    *   **Feature Maps:** The output of convolutional layers, representing the detected features in the input image.
*   **Pooling Layers:** Reduce the spatial dimensions of feature maps, reducing the number of parameters and improving robustness to small shifts and distortions.
    *   **Max Pooling:** Selects the maximum value in each pooling window.
    *   **Average Pooling:** Calculates the average value in each pooling window.
*   **Fully Connected Layers:** Layers that connect every neuron in one layer to every neuron in the next layer, used for classification or regression tasks after feature extraction.
*   **Applications of CNNs:** CNNs have revolutionized computer vision and image recognition. Key applications include:
    *   **Image Recognition:** Classifying images into different categories (e.g., cats vs. dogs).
    *   **Object Detection:** Identifying and locating objects within an image (e.g., detecting cars and pedestrians in a street scene).
    *   **Image Segmentation:** Partitioning an image into different regions or objects (e.g., separating the foreground from the background).
    *   **Medical Image Analysis:** Analyzing medical images for diagnosis and treatment planning.

## Recurrent Neural Networks (RNNs)

Recurrent Neural Networks (RNNs) are designed to handle sequential data, where the order of data points matters, such as text, time series, and audio.

*   **Architecture of RNNs:** RNNs have recurrent connections, allowing information to persist across time steps. They process sequential input one element at a time, maintaining a hidden state that captures information about past elements.
    *   **Recurrent Layers:** Layers in RNNs that process sequential input and update the hidden state.
    *   **Hidden State:** A vector that summarizes the information from past time steps, allowing RNNs to remember context.
*   **LSTM and GRU Units:** Vanishing gradient problem in traditional RNNs limits their ability to learn long-term dependencies. LSTM (Long Short-Term Memory) and GRU (Gated Recurrent Unit) are advanced RNN units that address this issue.
    *   **LSTM (Long Short-Term Memory):** Introduces memory cells and gates (input, output, forget gates) to control the flow of information and enable learning long-term dependencies.
    *   **GRU (Gated Recurrent Unit):** A simplified version of LSTM with fewer gates (update and reset gates), often performing comparably to LSTMs with fewer parameters.
*   **Applications of RNNs:** RNNs are widely used in natural language processing and time series analysis. Key applications include:
    *   **Natural Language Processing (NLP):**
        *   **Text Generation:** Generating human-like text (e.g., chatbots, language models).
        *   **Machine Translation:** Translating text from one language to another.
        *   **Sentiment Analysis:** Determining the sentiment (positive, negative, neutral) of text.
    *   **Time Series Analysis:**
        *   **Stock Price Prediction:** Predicting future stock prices based on historical data.
        *   **Weather Forecasting:** Predicting future weather conditions.
        *   **Anomaly Detection:** Identifying unusual patterns in time series data.
    *   **Speech Recognition:** Converting spoken language into text.
