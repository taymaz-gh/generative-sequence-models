## Introduction

This project explores two major areas of deep learning:

1. **Generative modeling** using convolutional autoencoders, Variational Autoencoders (VAEs), and Generative Adversarial Networks (GANs);
2. **Sequence-to-sequence learning** using recurrent neural networks for arithmetic reasoning across text and image modalities.

### Generative Models

The generative-modeling part uses an anime-face dataset containing 135,027 images. A subset of 22,000 RGB images was sampled, shuffled, normalized, and reshaped to 96 × 96 × 3 for model training.

Three architectures were investigated:

- **Convolutional Autoencoder (CAE)** as a reconstruction baseline;
- **Variational Autoencoder (VAE)** for probabilistic latent-space learning and image generation;
- **Generative Adversarial Network (GAN)** for adversarial image synthesis.

The CAE was used to study reconstruction quality and tune architectural parameters such as latent dimension, number of filters, number of upsampling/downsampling layers, and batch size.

For the VAE, the model learns a continuous latent distribution through a reconstruction term combined with KL-divergence regularization. The GAN instead trains a generator and discriminator in an adversarial objective.

After training, latent-space interpolation was performed by sampling two random latent vectors and linearly interpolating between them. The resulting image sequences illustrate how each model represents the learned image manifold.

The VAE produced smoother but generally blurrier images, while the GAN generated sharper outputs but showed greater training instability and occasional artifacts.

### Sequence-to-Sequence Learning

The second part investigates whether recurrent neural networks can learn arithmetic rules rather than simply memorize input-output pairs.

The dataset contains approximately 20,000 addition and subtraction queries involving integers up to two digits. Inputs and outputs are represented either as character sequences or sequences of MNIST-style digit images.

Three mapping problems were studied:

- **Text-to-Text:** arithmetic expressions represented as one-hot encoded character sequences;
- **Image-to-Text:** sequences of digit/operator images mapped to textual answers;
- **Text-to-Image:** textual arithmetic queries mapped to generated image sequences representing the answer.

The baseline text-to-text model uses an encoder–decoder LSTM architecture. Experiments were conducted using progressively smaller training sets to assess whether the model learned general arithmetic principles or merely memorized examples.

Prediction errors were categorized into several interpretable types, including sign errors, overflow errors, carry/borrow errors, single-digit errors, magnitude errors, and formatting errors.

For image-to-text modeling, ConvLSTM architectures were investigated to jointly capture spatial and temporal structure. An alternative architecture using a `TimeDistributed` CNN encoder followed by an LSTM decoder substantially improved performance, reaching approximately **93.5% test accuracy**.

The effect of model depth was also examined by stacking additional LSTM layers in the encoder and decoder. For the text-to-text task, a 2-layer encoder and 2-layer decoder achieved approximately **99.84% test accuracy** and eliminated carry-related errors in the reported experiments.

For text-to-image generation, the decoder reconstructs MNIST-like output frames using learned spatial feature maps and transposed convolutions. The generated outputs were evaluated visually and showed correct overall positioning but softer and blurrier digit shapes than the true images.

The project therefore combines generative modeling, latent-space analysis, sequence modeling, multimodal learning, recurrent architectures, model-depth analysis, and structured error analysis.

---

## Summary

**Deep Learning – Generative Models & Sequence Learning:** Trained convolutional autoencoders, VAEs, and GANs (`TensorFlow`, `Keras`) for image reconstruction, generation, and latent-space interpolation, and developed encoder–decoder sequence models using LSTM, ConvLSTM, and TimeDistributed CNN architectures for text-to-text, image-to-text, and text-to-image arithmetic tasks, including generalization analysis, model-depth experiments, and structured error analysis.