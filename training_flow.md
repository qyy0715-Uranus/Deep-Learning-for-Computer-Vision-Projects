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

    %% Losses (高亮红色)
    Recon_ut -.->|L_recon_t| Loss1((Loss 1))
    Latent_zt_prime -.->|L_latent| Loss2((Loss 2))
    Output_ut_prime -.->|L_pred| Loss3((Loss 3))
    
    %% 样式配置
    
    %% 1. Encoders - 淡蓝色
    style Enc fill:#B0E2FF,stroke:#333,stroke-width:2px
    style Enc2 fill:#B0E2FF,stroke:#333,stroke-width:2px
    
    %% 2. Decoders - 浅绿色
    style Dec fill:#C1FFC1,stroke:#333,stroke-width:2px
    style Dec2 fill:#C1FFC1,stroke:#333,stroke-width:2px
    
    %% 3. Approximator - 深紫色 (最核心)
    style App fill:#8A2BE2,stroke:#000,stroke-width:3px,color:#fff
    
    %% 4. Losses - 亮橙红色
    style Loss1 fill:#FF4500,stroke:#333,stroke-width:2px,color:#fff
    style Loss2 fill:#FF4500,stroke:#333,stroke-width:2px,color:#fff
    style Loss3 fill:#FF4500,stroke:#333,stroke-width:2px,color:#fff

    %% 5. 潜在变量节点 - 保持中性
    style Latent_zt fill:#fff,stroke:#333
    style Latent_zt_prime fill:#fff,stroke:#333
    style Latent_target fill:#fff,stroke:#333
