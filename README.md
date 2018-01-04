This repository contains some extracts of the code in Python and Tensorflow used to study a progression of Alzheimer's Disease using Deep Generative Models (Variational Autoencoders, Conditional Adversarial Autoencoders).

The aim of this thesis is to predict the progression of Alzheimer’s Disease in Structural Magnetic Resonance Imaging using Deep Generative methods. To the best of our knowledge, this is the first attempt to generate the progression of the disease using deep learning methods.

Alzheimer’s disease is the most common cause of dementia worldwide, and this tendency is predicted to become even more marked in the next years, with the global aging of the population. While several therapies are currently being studied, they are mostly tested when patients experience the first symptoms of cognitive impairment, indicating that the disease is already in an advanced stage. A robust model able to predict the development of the disease and its influence on specific regions of the brain would guarantee higher chances to slow down, stop or even prevent the disease.

The problem of classifying a brain scan into Alzheimer’s Disease (AD), Mild Cognitive Impairment (MCI) and Normal Control (NC) has already been tackled extensively and quite successfully by the machine learning community. More recently, deep learning methods have also been applied to classification and feature extraction tasks, making extensive use of their ability to produce hierarchical feature representations. On the other hand, the idea of generating a progression (or regression) in time starting from an input image was never successfully applied to MRI scans for the study of AD, as opposed to other imaging fields.

For this study, about 950 sMRI volumes have been gathered. Structural MRI is targeted as the input data type for its being relatively cheap and non-invasive for the patient. It is thus imaginable, in the future, to use this type of exam in a more established pipeline, where patients that show a predisposition towards this type of dementia can undergo frequent examining sessions since a young age, in order to track effectively the development of the disease and act early on with proper treatments.

It must be noted however, that the progression of Alzheimer’s disease depends on a number of different factors including, but not limited to, genetics, cardiovascular conditions, morphological characteristics and in general personal health history. However, the sMRI scans used for this study are only accompanied by age, gender and Mini-Mental State Examination (MMSE) scores, which makes the problem of generating a progression in time even more challenging.

This work can be divided into two parallel tracks, based on different pre-processing techniques applied to the input volumes.
A first approach leverages 2D brain slices. Several techniques were attempted to find those slices that are most relevant with respect to the disease diagnosis, and to extract them along the three main axes (axial, sagittal, coronal). Following this approach, we extract slices from the centre of the brain and from those areas where the hippocampus, a key element in AD diagnosis, is maximally present.

Since the importance of shapes and volumes is widely recognised in order to understand the main characteristics of AD-affected brains, we focus also on the segmentation of sMRI scans using a Fully Convolutional neural network, resulting in 3D binary maps of the most relevant organs for AD diagnosis (such as hippocampus and ventricles).

We use these 2D slices and 3D shapes as inputs to generative models, for their ability to learn meaningful latent representations that encode the most relevant features, and to generate images with certain characteristics, or belonging to particular classes. To this end, we use a Convolutional Variational AutoEncoder (CVAE) and Conditional Adversarial AutoEncoder (CAAE). These models integrate both supervised and unsupervised approaches.

The CVAE is able to learn a manifold that encodes the most distinctive brain features and can be walked to progress them in terms of shape, size and morphological characteristics. This latent representation however is still unable to cluster the subjects into the three distinct classes based on their diagnosis. For what concerns 2D slices, this behaviour can be explained from a theoretical standpoint considering the limitations of the automatic extraction of slices; from a 3D perspective, it must be noted that it is extremely hard, even for an expert neuroradiologist, to discriminate a diseased patient from a healthy one simply by analysing single shapes. When aided by the injection of supervised information, the CVAE is able to learn a more meaningful organization of the latent space, where labels and latent variables are correlated.

In order to produce a progression in time of the subjects, a CAAE is implemented. This approach integrates the standard Autoencoder with Generative Adversarial Networks. Once again, the network first learns a manifold that can encode the most relevant features in the data, then learns to generate very realistic images starting from these encodings. In this case too, supervised information helps the network understand the link between imaging input, age and classification. This way, the network is able draw a progression in time, which is evaluated qualitatively on 2D slices and quantitatively on 3D shapes. For what concerns 2D slices, the network generates a progression where global cerebral volume is decreasing, grey matter becomes more marked and ventricles enlarged, but it still lacks general consistency in terms of individual, morphological characteristics and overall coherency in the progression. Results on 3D shapes are more encouraging: we obtain a statistically significant decrease in the shape of the hippocampus over time, that is more marked for AD patients with respect to NC subjects, which is confirmed by literature.