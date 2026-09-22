The link to the install
cloud.google.com/sdk/docs/install

On Deabian/Ubuntu 

```bash
sudo apt-get update
```

This check If you have ca-certif, gnu, curl
```bash
sudo apt-get install ca-certificates gnupg curl
```

Import the google Cloud key :
```bash
curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo gpg --dearmor -o /usr/share/keyrings/cloud.google.gpg
```
This cmd Depends on the Os version

Add the gcloud CLI distribution URI (Uniform Resource Identifier) Its used to identify a network/Web ressource.
```bash
echo "deb [signed-by=/usr/share/keyrings/cloud.google.gpg] https://packages.cloud.google.com/apt cloud-sdk main" | sudo tee -a /etc/apt/sources.list.d/google-cloud-sdk.list
```

Install The actual CLI 
```bash
sudo apt-get update && sudo apt-get install google-cloud-cli
```

For Docker
```bash
RUN echo "deb [signed-by=/usr/share/keyrings/cloud.google.gpg] https://packages.cloud.google.com/apt cloud-sdk main" | tee -a /etc/apt/sources.list.d/google-cloud-sdk.list && curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | gpg --dearmor -o /usr/share/keyrings/cloud.google.gpg && apt-get update -y && apt-get install google-cloud-cli -y
```