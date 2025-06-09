# Projeto Apache no K3s

Este repositório contém os arquivos e passos para implantar um aplicativo Apache simples em um cluster K3s (Kubernetes).

## Resumo do Progresso

1.  **Criação da Imagem Docker:**
    * Um `Dockerfile` foi criado para construir uma imagem Docker com o Apache e um arquivo `index.html` customizado.
    * A imagem foi construída e enviada para o Docker Hub (ou carregada diretamente no K3s).

2.  **Deployment do Kubernetes:**
    * Um arquivo `deployment.yaml` foi criado para definir um Deployment, garantindo que o aplicativo Apache seja executado no cluster.
    * O Deployment gerencia as réplicas dos pods (inicialmente 1, depois escalado para 3).

3.  **Service do Kubernetes:**
    * Um arquivo `service.yaml` foi criado para expor o aplicativo Apache.
    * Inicialmente, um Service do tipo `NodePort` foi usado para facilitar o acesso via IP do nó e porta alta.
    * Posteriormente, um Service do tipo `ClusterIP` foi recomendado para uso com Ingress.

4.  **Ingress do Kubernetes:**
    * Um arquivo `ingress.yaml` foi criado para expor o aplicativo na porta 80, utilizando o Traefik (Ingress Controller padrão do K3s).
    * Foi necessário configurar o DNS (ou o arquivo `/etc/hosts`) para acessar o aplicativo pelo nome de host definido no Ingress.

5.  **Armazenamento Persistente (Opcional):**
    * A opção de usar `hostPath` volumes foi explorada para mapear um diretório do host diretamente para o pod do Apache (para persistência do `index.html`).
    * A abordagem recomendada de `PersistentVolumeClaim` (PVC) e `PersistentVolume` (PV) com o `local-path-provisioner` também foi apresentada.

6.  **Escalabilidade:**
    * O comando `kubectl scale` foi usado para aumentar o número de réplicas do Deployment.

## Próximos Passos (Sugestões)

* Configurar HTTPS com Let's Encrypt (Cert-Manager).
* Implementar monitoramento com `kubectl top nodes` e `kubectl top pods`.
* Explorar Namespaces para organizar os recursos do Kubernetes.
* Automatizar o processo de deployment com um script (como o `deploy_apache_app.sh` fornecido).
