# Training Flow

```mermaid
graph TD
    %% 核心数据流
    Input_ut[Input: u_t] --> Enc[Encoder]
    Enc -->|zt| Latent_zt[z_t]
    Latent_zt --> App[Approximator]
    App -->|zt'| Latent_zt_prime[z_t']
    Latent_zt_prime --> Dec[Decoder]
    Dec -->|u_hat_t'| Output_ut_prime[Prediction: u_hat_t']

    %% 辅助约束分支 1: Autoencoder Reconstruction
    Latent_zt --> Dec2[Decoder]
    Dec2 -->|u_hat_t| Recon_ut[Reconstructed: u_hat_t]
    
    %% 辅助约束分支 2: Latent Space Matching
    Input_ut_prime[Target: u_t'] --> Enc2[Encoder]
    Enc2 -->|z_hat_t'| Latent_target[Target Latent: z_hat_t']

    %% Losses
    Recon_ut -.->|L_recon_t| Loss1((Loss 1))
    Latent_zt_prime -.->|L_latent| Loss2((Loss 2))
    Output_ut_prime -.->|L_pred| Loss3((Loss 3))
    
    %% 样式
    style Loss1 fill:#f9f,stroke:#333
    style Loss2 fill:#f9f,stroke:#333
    style Loss3 fill:#f9f,stroke:#333
    style App fill:#ff9,stroke:#333
