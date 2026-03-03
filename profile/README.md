🎬 ClipToZip

ClipToZip é uma aplicação que permite ao usuário fazer upload de um vídeo, processá-lo automaticamente para extração de frames (imagens) e disponibilizar essas imagens compactadas em um arquivo .zip para download.

O projeto foi pensado para ser escalável, assíncrono e cloud-native, utilizando serviços da AWS como Amazon S3 e processamento em background.

📌 Visão Geral da Solução

Fluxo principal da aplicação:

O usuário realiza o upload de um vídeo pela aplicação.

O vídeo é armazenado em um bucket Amazon S3.

Um processo assíncrono é disparado para:

Processar o vídeo

Extrair imagens (frames)

Compactar as imagens em um arquivo .zip

O arquivo .zip final é armazenado no S3.

O usuário recebe um link para download do arquivo gerado.

🏗️ Arquitetura (Visão Conceitual)

Frontend / API
Responsável pelo upload do vídeo e consulta do status do processamento.

Amazon S3

Bucket de entrada: armazenamento dos vídeos enviados

Bucket de saída: armazenamento dos arquivos .zip gerados

Processamento Assíncrono

Serviço responsável por consumir o vídeo do S3

Extrair frames

Gerar o arquivo .zip

Enviar o resultado para o S3

O processamento é desacoplado da requisição do usuário para garantir escalabilidade e evitar bloqueio da API.

🧰 Tecnologias Utilizadas
Backend

Java (Spring Boot)

Processamento de vídeo (ex: FFmpeg)

Arquitetura orientada a eventos / assíncrona

Cloud (AWS)

Amazon S3 – armazenamento de vídeos e arquivos zip

IAM – controle de permissões

(Opcional) SQS / SNS / Lambda / ECS – para orquestração e escalabilidade do processamento

Outros

ZIP compression

Upload multipart

Logs e monitoramento
