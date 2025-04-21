This repo contains the project submission for the Black Box Interpretability Hackathon (Jan 19th, 2025) hosted by the Society for Technological Advancement (SoTA) at the Entrepreneur First (EF) offices in London. 

Our whole approach operates under the assumption that we have some black box image diagnostic  classifier which sorts into disease/healthy classes. For the sake of simplicity we considered pneumonia cases in x-ray scans to validate the approach.
![image](https://github.com/user-attachments/assets/ebf36b69-e4c9-4d8f-b371-c2467d921246)

Instead of attention or gradient based saliency maps (which among many problems can only measure sensitivity not causal relationships!), we cooked up a latent-space method to generate diagnostically-relevant attribution maps. The latent-space method was inspired from: https://www.nature.com/articles/s41598-024-81646-x

Leveraging RadBERT embeddings (BERT fine-tuned on radiology reports) into the latent space of a diffusion autoencoder, we integrated the embeddings to condition a denoising U-Net to produce (zero-shot) healthy counterfactuals from the diseased image prior.We then took the relative difference between the ground truth and the synthetic counterfactual. We assigned difference scores based on structural similarity, finally converting into an interpretable attribution map, mapping the extent of COVID in the example below:
![image](https://github.com/user-attachments/assets/b160969a-5784-4bef-ac29-d33d2cfcc5db)



