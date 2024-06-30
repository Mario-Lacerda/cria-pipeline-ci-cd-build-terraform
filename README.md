# Desafio Dio - Criando Pipeline de CI/CD com Cloud Build e Terraform



Um pipeline de CI/CD (integração contínua e entrega contínua) automatiza o processo de desenvolvimento de software, desde a escrita do código até a implantação em produção. O Cloud Build é um serviço do Google Cloud que pode ser usado para criar pipelines de CI/CD. O Terraform é uma ferramenta de provisionamento de infraestrutura que pode ser usada para provisionar e gerenciar recursos em nuvem.



### **Pré-requisitos**

- Projeto do Google Cloud
- Cloud Build ativado
- Terraform instalado



### **Passos**



### **1. Configurar o Cloud Build**



- Crie um arquivo `cloudbuild.yaml` com o seguinte conteúdo:

yaml



```yaml
steps:
  - name: terraform
    entrypoint: terraform
    args: [init, apply]
  - name: gcloud
    entrypoint: gcloud
    args: [app, deploy]
```



- Substitua `[app]` pelo nome do seu aplicativo do Google Cloud.



### **2. Configurar o Terraform**



- Crie um arquivo `main.tf` com o seguinte conteúdo:

plaintext



```plaintext
resource "google_compute_instance" "default" {
  name         = "my-instance"
  machine_type = "n1-standard-1"
  zone         = "us-central1-a"
  boot_disk {
    initialize_params {
      image = "debian-cloud/debian-11"
    }
  }
  network_interface {
    network = "default"
  }
}
```



- Substitua `[network]` pelo nome da sua rede do Google Cloud.



**3. Executar o pipeline**



- Execute o seguinte comando para executar o pipeline:

plaintext



```plaintext
gcloud builds submit --config cloudbuild.yaml
```



### **Conclusão**



Seguindo esses passos, você criou um pipeline de CI/CD que provisiona uma instância do Compute Engine usando o Terraform e implanta seu aplicativo nela usando o Cloud Build.
