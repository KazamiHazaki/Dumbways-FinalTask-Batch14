# Dumbways-FinalTask
***

Task List

1. [Cloud Computing](https://github.com/KazamiHazaki/Dumbways-FinalTask-Batch14#-cloud-computing-)
2. [SSH](https://github.com/KazamiHazaki/Dumbways-FinalTask-Batch14#-ssh-)
3. [Repository](https://github.com/KazamiHazaki/Dumbways-FinalTask-Batch14#-repository-)
4. [Deployment](https://github.com/KazamiHazaki/Dumbways-FinalTask-Batch14#-deployment-)
5. [CI/CD](https://github.com/KazamiHazaki/Dumbways-FinalTask-Batch14#-cicd-)
6. [Monitoring](https://github.com/KazamiHazaki/Dumbways-FinalTask-Batch14#-monitoring-)
7. [Web Server](https://github.com/KazamiHazaki/Dumbways-FinalTask-Batch14#-web-server-)
8. [Microservices](https://github.com/KazamiHazaki/Dumbways-FinalTask-Batch14#-microservices-)


# <h1> CLOUD COMPUTING </h1>

***

***

#  <h2>Create VM </h2>

Lalu kita persiapkan 3 VM dengan spesifikasai berikut

- Appserver - 2 vCPU, 2GB RAM
- Gateway - 1 vCPU, 1GB RAM
- Monitoring - 2 vCPU, 2GB RAM
- 20 GB Untuk semua VM
- Ubuntu 20.04 LTS 

menggunakan platfrom cloud IDCLoudHost


![image](https://user-images.githubusercontent.com/56806850/208279361-6b9ed68d-2fc6-4e3c-a253-9b6d82ddbfd3.png)

kemudian untuk isi usernya sesuai dengan keinginan, dan isi password, dan beri nama VM pada resource name 

![image](https://user-images.githubusercontent.com/56806850/208279379-22e3d500-8035-4b22-a3aa-73a34a3cc052.png)

lakukan hal yg sama untuk ke 3 VM di atas.

***

***
***

# <h1> SSH </h1>

***
***


#  <h3> Create SSH key </h3>

setelah selesai membuat 3 VM kita buat SSH key yang akan di gunakan untuk mengakses server tanpa password.

pada windows bisa menggunakan CMD/Shell lalu ketikan `ssh-keygen`, kita buat secara default tanpa menggunakan password langsung tekan enter saja pada saat ditanyakan passphrase.

![image](https://user-images.githubusercontent.com/56806850/208279672-a996bef8-f350-4bff-af0c-d23a95012140.png)

lalu bisa di cek pada folder `.ssh` ssh yg sudah dibuat.

![image](https://user-images.githubusercontent.com/56806850/208279714-a0442c0d-a23e-429a-b70b-c4f2362babbf.png)

setelah membuat ssh-key, key ini belum bisa langsung di gunakan untuk mengaksesnya, kita harus mengirim ssh key ini ke server yg ingin di tuju dengan cara menggunakan `ssh-copy-id`

![image](https://user-images.githubusercontent.com/56806850/208279968-0db6dd31-f01f-404f-bc00-fe9fd41a7a04.png)


dengan cara seperti di atas.

```shell
ssh-copy-id -i <lokasisshkey> <user>@<IPServer>
```

lalu kita coba akses langsung menggunakan ssh

![image](https://user-images.githubusercontent.com/56806850/208279980-5d52a528-91db-4c36-8d63-a9f82511dae4.png)

vps sudah bisa di akses langsung tanpa menggunakan password. lakukan hal yang sama pada server lainnya

kita simpan ssh ini untuk digunakan nanti lagi.

***
***

# <h1> Repository </h1>

***
***

# <h2> Menghubungkan Git dengan GPG key github </h2>
Sebelum kita menggunakan git kita hubungkan terlebih dahulu dengan github akun kita, disin akan menggunakan GPG Key dari github.

pertama buat terlebih dahulu kunci nya buka pada bagian settings

![image](https://user-images.githubusercontent.com/56806850/208430705-92652891-b012-4db4-a4b3-0fbe4635879d.png)

kemudian scroll tab bagian kiri bawah sendiri, pilih Developer settings

![image](https://user-images.githubusercontent.com/56806850/208430785-7a56ea41-cb90-4f30-b922-84537aac50c7.png)

pilih Personal access tokens bagian `Tokens(classic)`

![image](https://user-images.githubusercontent.com/56806850/208430869-af6fe8a3-3a3c-48c8-9f03-b6abdcf01227.png)

generate new token

![image](https://user-images.githubusercontent.com/56806850/208430895-fc6a82d0-4c7b-4b86-8a52-8e85ecad10c4.png)

beri nama kunci dan settigns expiration keynya, lalu centang semua checklist di bawah 

![image](https://user-images.githubusercontent.com/56806850/208431136-647c5696-fcbb-43ec-a5fe-c81b8991636e.png)

setelah itu kita copy kuncinya 

![image](https://user-images.githubusercontent.com/56806850/208431218-aac8729c-4bed-4d05-a35d-43b465eda0bc.png)

setelah di copy tambahkan ke git cli. 

```shell
git config user.name "<username github>"
git config user.email "<username github>"

```

dan tambah kan credential cache agar kita tidak perlu lagi menambahkan kunci setiap kita ingin menggunakan git push

```shell
git config credential.helper cache
```

setelah menambahkan cache, kita bisa memasukan kunci token tadi saat kita menggunakan push, dan paste pada password

```shell
$ git push http://example.com/repo.git
Username: <type your username>
Password: <type your password>
```

***

#  <h2>Private Repository </h2>
Pertama Marikita Siapkan Terlebih dahulu Private Repository

![image](https://user-images.githubusercontent.com/56806850/208279288-b8b380a7-5838-42f0-a270-7c5defad4c6b.png)


Kemudian Pilih repository sebgai Private
 
![image](https://user-images.githubusercontent.com/56806850/208279290-0d1bbd14-ac9b-45ac-ab42-534d541815d1.png)


setelah membuat repository baru kita tambahkan file repository dari 2 github dumbways ke repository private kita

- https://github.com/dumbwaysdev/wayshub-frontend
- https://github.com/dumbwaysdev/wayshub-backend 


download terlebih dahulu ke 2 repository tersebut dan kita upload ke repository baru dengan menggunakan git clone

```shell
git clone https://github.com/dumbwaysdev/wayshub-backend.git
git clone https://github.com/dumbwaysdev/wayshub-frontend.git
```

![image](https://user-images.githubusercontent.com/56806850/208422483-9a1d6a94-b305-45f5-9859-9579a1ba3474.png)

2 repository sudah di download dan ada di folder kita 

![image](https://user-images.githubusercontent.com/56806850/208422587-2bd31568-a510-4338-a6df-f336ca4467ab.png)

tambahkan remote git dari repository kita ke cli git

```shell
git remote add origin https://github.com/KazamiHazaki/Dumbways-FinalTask
```
![image](https://user-images.githubusercontent.com/56806850/208423063-8420bedc-2002-4340-b307-eb86dac32b32.png)


repository kita sudah ada di cli git

```shell
git remote -v
```

![image](https://user-images.githubusercontent.com/56806850/208423127-d850d10a-1dfe-4a11-a7ed-0a5f6a1f849b.png)


kemudian setelah kita remote repository, kita add file ke repository kita.

![image](https://user-images.githubusercontent.com/56806850/208423753-8c6aaa6b-dea4-40ab-acd8-666f81d257bf.png)

pertama kita tambahakan semua file yg ada di direktori saat ini ke git, dan lakukan commit 

```shell
git add .
git status #check status perubahan pada git

git commit -m "add wayshub" # menambahkan tanda perubahan pada git
git push origin main
```
setelah upload file ke repository kita. kita buat 3 branch baru yaitu :


- Staging
- Production


![image](https://user-images.githubusercontent.com/56806850/208429952-47bcebbb-14f3-4ff1-9da5-4df4c238d101.png)

```shell
git branch Staging
git branch Production 
```
kedua command di atas digunakan untuk membuat branch baru.lalu kita cek menggunakan `git branch`

![image](https://user-images.githubusercontent.com/56806850/208429899-1d18a99a-897a-4d65-bf4c-4a44c78614f9.png)

setelah membuat branch baru kita push dari lokal machine kita ke 2 branch terseebut pertama pindah ke branch lalu push

```shell
git checkout staging
```
![image](https://user-images.githubusercontent.com/56806850/208430119-f4b74d24-5171-4b71-928d-0126f41afe05.png)

maka kita sudah pindah ke branch Staging. lalu kita push

![image](https://user-images.githubusercontent.com/56806850/208430180-52e4d3ec-8368-42de-984f-f0ea4221e246.png)

setelah itu kita bisa cek pada repository kita jika branch sudah di tambahkan.

![image](https://user-images.githubusercontent.com/56806850/208430277-c5b4a653-4ec9-4016-b60f-35bcd7cbf680.png)

***

# <h1> Deployment </h1>
***

<h2> Install Docker </h2>

menginstall apt package dari dari HTTPS 

```shell
sudo apt-get update
sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```

dan menambahkan docker GPG key

```shell
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

dan mensetting repository 

```shell
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

![image](https://user-images.githubusercontent.com/56806850/208650940-a47cb3ca-2083-4041-93b2-ee74cc4ca39b.png)


kemudian kita install docker 

```shell
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
```

![image](https://user-images.githubusercontent.com/56806850/208651425-b45ee35f-729f-4f90-849b-5c03ab053e4e.png)


setelah melakukan installasi docker, kita tambahakan docker ke group user, agar ktia bisa menggunakan command docker tanpa menggunakan Sudo

```shell 

sudo usermod -aG docker $USER
su - ${USER}
```

```shell
groups
```

![image](https://user-images.githubusercontent.com/56806850/208653682-80c44e7b-359c-4f97-9068-56ad69d6b2a4.png)

jika sudah muncul docker di groups maka bisa log out

kemudian log out dari user dan login kembali


setelah log out kita bisa menggunakan command docker tanpa menggunakan SUDO 

![image](https://user-images.githubusercontent.com/56806850/208654244-c720fb85-7a57-47d5-8601-ba16367e963e.png)

<h3> Login Docker Hub Di CLI </h3>

setelah install docker kita hubungkan akun docker hub ke server

```shell
dcoker login
```

![image](https://user-images.githubusercontent.com/56806850/208659821-8602e46e-633f-4d2d-8e1c-cd8a1779cb24.png)

masukkan username dan password


<h3> Integration Database with webapp </h3>

<h4> Setup Backend And Database </h4>

pada integrasi web app disini akan menggunakan docker, sebelum itu kita persiapkan terlebih dahulu file yg dibutuhkan

- dockerfile backend, frontend
- docker-compose.yml


isi dari dockerfile merupakan node js dan mengcopy backend menjadi image, yang akan di upload ke docker hub, isi dari dockerfile seperti berikut.


`dockerfile frontend`
```shell
FROM node:10.24-alpine
WORKDIR /app
COPY backend .
RUN npm install
RUN npm install -g sequelize-cli
RUN npx sequelize db:migrate
EXPOSE 5000
CMD ["npm","start"]
```

kemudian untuk docker compose kita siapkan terlebih dahulu MYSQL

`docker-compose.yml`
```shell
version: "3.8"
services:
   mysql_db:
    image: mysql
    container_name: wayshub_mysql_db
    restart: always
    stdin_open: true
    ports:
     - "3306:3306"
    environment:
     - MYSQL_ROOT_PASSWORD=root
     - MYSQL_USER=aziz
     - MYSQL_PASSWORD=Wayshub1
     - MYSQL_DATABASE=wayshub

    volumes:
     - "/home/aziz/web-app/database:/var/lib/mysql"
     
     
      
```
lalu jalakan docker compose untuk menginstall mysql di dalam docker.
![image](https://user-images.githubusercontent.com/56806850/208846484-3670c1d8-723a-406b-b45e-f791a58dfe1e.png)

setelah membuat mysql. kita persiapkan docker file mennjadi image dan kita push ke docker hub.


sebelum membuild dockerfile kita rubah terlebih dahulu config pada backend, ubah sesuai environment yg di gunakan pada docker compose dan ganti host menjadi IP host

```shell
"development": {
    "username": "aziz",
    "password": "Wayshub1",
    "database": "wayshub",
    "host": "103.13.207.87",
    "dialect": "mysql"
  }
```

![image](https://user-images.githubusercontent.com/56806850/208847041-426d24f1-e932-4441-9798-6fa3b0bd55c4.png)

masuk ke direktori yg sama dengan dockerfile kemudian build 

```
docker build -t kazamisei98/wayshub-be:1.0 .
```
![image](https://user-images.githubusercontent.com/56806850/208850150-342f5a9a-d816-4fd4-b44e-0ac67c0f1337.png)

setelah di build coba di cek kembali di dalam database apakah sudah ada migrasi database atau belum dengan cara mengakses docker mysql

```shell
docker exec -it wayshub_mysql_db /bin/bash
```
setelah masuk ke docker mysql, akses mysql dengan 

```shell
mysql -u aziz -p
```
masukan passsword yg sama pada environment docker compose.

lalu gunakann database wayshub dan cek table

```shell
show databases;
use wayshub;
show tables;
```
jika sudah ada tables seperti di bawah maka migrasi sudah berhasil


![image](https://user-images.githubusercontent.com/56806850/208850478-152d1011-e62c-4d7b-a982-af8d66558ea4.png)

kemudian setelah berhasil membuat images

![image](https://user-images.githubusercontent.com/56806850/208851804-e5efb4ca-3124-44b8-ad86-27a157cb6799.png)

kita push ke docker hub 

```shell
docker push kazamisei98/wayshub_be:1.0 
```

![image](https://user-images.githubusercontent.com/56806850/208853653-e2b76526-9a68-4ef9-915e-ccb8bbf75d53.png)

setelah mengupload images ke docker hub kita bisa menggunakannya untuk membuat docker images tanpa download repository wayshub-backend

tambahkan images kazamisei98/wayshub_be ke docker compose

```shell
  wayshub_be:
    image: kazamisei98.wayshub_be:1.0
    container_name: wayshub_be
    ports:
     - 5000:5000
    depends_on:
     - mysql_db
```

kemudian docker bisa di compose kembali 

![image](https://user-images.githubusercontent.com/56806850/208856680-27df481f-3b8b-4715-8bef-98bfd063a71a.png)

jika tidak ada masalah maka contaienr wayshub_be dan mysql akan berjalan dengan baik tanpa ada error atau container berhenti berjalan.

<h4> Setup Frontend </h4>

untuk frontend buat terlebih dahulu dockerfile dan ubah alamat pada file api.js yg ada di src/config 

rubah terlebih dahulu api.js menggunakan IP server, kemudian save file 

![image](https://user-images.githubusercontent.com/56806850/208960551-62177f99-e8fb-4d02-aa79-ab84aa20f8cb.png)

setelah merubah API buat dockerfile.

`Dockerfile Frontend`

```shell

FROM node:10.24.1-alpine
WORKDIR /usr/src/app
COPY . .
RUN npm install
EXPOSE 3000
CMD ["npm","run","start"]
```
lalu build dengan tag 

```shell
docker build -t kazamisei98/wayshub_fe.1 .
```

![image](https://user-images.githubusercontent.com/56806850/208960069-d0e195e6-916f-499e-a479-c92d994b4423.png)

setelah build images jadi tambahkan services frontend pada docker compose

![image](https://user-images.githubusercontent.com/56806850/208960389-0c317c91-577d-48f8-b801-99fe09d88d53.png)

`docker-compose.yml`
```shell
   frontend:
    image: kazamisei98/wayshub_fe:1.1
    container_name: wayshub_fe
    ports:
     - 3000:3000
```

dan jalankan compose.

![image](https://user-images.githubusercontent.com/56806850/208960724-cea62adf-00d0-489b-a491-1c659cce884c.png)

kemudian kita bisa cek melalui IP:3000 untuk frontend

![image](https://user-images.githubusercontent.com/56806850/208961383-8b5d0793-ae4d-43fd-bca1-99cb00141599.png)

terlihat pada gambar di atas backend sudah bekerja dengan baik sehingga bisa signup melalui frontend

dan bias login setelah melakukan registrasi 

![image](https://user-images.githubusercontent.com/56806850/208961631-f24d2ee3-3bb4-47f9-9be7-0a4a51f94378.png)



# <h1> CI/CD </h1>
***


<h2> Install jenkins on docker </h2>

pertama buat docker-compose terlebih dahulu 

```shell
version: '3.8'
services:
  jenkins:
   image: jenkins/jenkins:lts
   privileged: true
   ports:
   - "8080:8080"
   - "50000:50000"

   volumes:
    - "/home/aziz/jenkins:/var/jenkins_home"


```

![image](https://user-images.githubusercontent.com/56806850/209060499-70ec1331-e6de-4f2a-9f18-721e41f4f8fd.png)

jalankan dengan docker compose 

![image](https://user-images.githubusercontent.com/56806850/209060588-b4e96adb-b9b5-4471-a8dd-936c2b980942.png)


pada saat pertamakali akan diminta untuk memasukan password yang sudah di generate secara random oleh jennkins yg letaknya ada di 

```shell
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```
masukkan password tersebut untuk bisa mengakses jenkins.

![image](https://user-images.githubusercontent.com/56806850/209060690-ea963d24-b001-41f2-910d-7498bedb0984.png)



pada installasi plugin pilih reccomennded plungin.setelah installasi plugin selesai maka akan diarahkan untuk membuat akun admin

![image](https://user-images.githubusercontent.com/56806850/209060964-8ff79089-6a06-4d4c-8233-94e3d46d4c1a.png)




instance config biarkan seperti ini 

![image](https://user-images.githubusercontent.com/56806850/206362098-ab8d705d-1d9d-44af-818e-16cd40103ff6.png)

dan jenkins sudah siap untuk di  gunakan 

![image](https://user-images.githubusercontent.com/56806850/206362135-8eb27679-ab41-43d7-965f-4c80f0a75765.png)

<h3> Add user Jenkins </h3>

setelah login ke jenkins tekan profile kemudian credentials

![image](https://user-images.githubusercontent.com/56806850/209423867-8c70f439-603a-496c-aa85-71b775efe9b9.png)


kemudian add credentials

![image](https://user-images.githubusercontent.com/56806850/209423886-e763a8a4-7d17-410f-8c19-f7e349a40f69.png)


lalu pilih ssh with private key
![image](https://user-images.githubusercontent.com/56806850/209424009-911f4d70-1cd0-499b-a356-e6f646a4f4af.png)


isi bagian ID menggunakan username login VPS

![image](https://user-images.githubusercontent.com/56806850/209423985-baec8f16-5b92-491b-bb3e-0eb1b0a15567.png)

isi bagian private key dengan mengcopy private key kemudian paste lalu di save


![image](https://user-images.githubusercontent.com/56806850/209424052-312cf8a0-09de-4ec1-9d5d-a281404ef55c.png)



lalu setelah mengisi credentials user pada jenkins dan memberi public key pada github coba gunakan build now dan kita lihat apakah berhasil buildnya

![image](https://user-images.githubusercontent.com/56806850/209431396-f05ab662-0979-4559-a33a-6a59d49db083.png)



<h3> Create multibranch Pipeline </h3>

ke bagian dashboard kemudian new item

![image](https://user-images.githubusercontent.com/56806850/209424210-38941b14-4cde-4d50-9c26-706c534f50f6.png)

masukan nama pipeline dan pilih multibranch pipeline

![image](https://user-images.githubusercontent.com/56806850/209424219-0a21894d-958a-4e23-9d5b-43e3154c60f0.png)

setelah itu tambahkan branch source menggunakan git 

![image](https://user-images.githubusercontent.com/56806850/209424421-db7c5968-337b-4d94-a496-40035d1882c0.png)

masukan link git hub menggunakan git lalu gunakan credentials yg sudah di buat tadi 

![image](https://user-images.githubusercontent.com/56806850/209424470-fb96c9ce-3c51-463d-9b5b-23eb634f9302.png)

<h3> autotrigger when commit </h3>

untuk mengaktifak fitur autotrigger dibutuhkan plugin tambahan yaitu multibranch scan webhook trigger

![image](https://user-images.githubusercontent.com/56806850/209424147-d43c9ff1-24a2-421b-bbdd-6a79630b6caa.png)

bisa di install melalui dashboard > manage jenkins > plugin manager install plugin tersebut  dan aktifakn pada multibranch pipeline 

setelah menginstall plugin aktifkan pada configuration multibranch pipeline 

![image](https://user-images.githubusercontent.com/56806850/209424486-5ee4c37d-3871-444b-bc66-11dab43ee284.png)
 
 setelah itu tambahkan link trigger pada webhook github 
 
 ![image](https://user-images.githubusercontent.com/56806850/209424622-aa9ee2b6-a51c-4b98-828f-7790d58c1728.png)
`http://154.26.155.62:8080/multibranch-webhook-trigger/invoke?token=mytoken`

![image](https://user-images.githubusercontent.com/56806850/209424668-af15a612-58fc-45bf-a3c7-c1ef39922dc5.png)

gunakan content type application/json kemudian di save

lalu berinama pada trigger token

<h2> menghubungkan github dengan jenkins menggunakan SSH </h2>

tambahkan plugin ssh 

![image](https://user-images.githubusercontent.com/56806850/209427531-43b003ca-726a-4f29-9082-d9e1aa08bfaf.png)

kemudian gunakan ssh private key dari yg sudah di buat di server jenkins menggunakan command `ssh-keygen`

copy privatekey dari file `.ssh/id_rsa`

```shell
cat .ssh/id_rsa
```

kemudian paste pada user jenkins

![image](https://user-images.githubusercontent.com/56806850/209427757-e70f92f0-4cae-44ae-accd-eb6f7811edfa.png)

lalu sesudah memberi privatekey pada jenkins pada repository github juga di beri ssh key menggunakan ssh key public



![image](https://user-images.githubusercontent.com/56806850/209427774-9634d99d-6802-4f79-bd38-3d6c84dc457c.png)

lalu scan secara manual


dan auto trigger berjalan 

![image](https://user-images.githubusercontent.com/56806850/209431573-70045bc8-bb99-44d9-a998-62c27a4ae76c.png)

<h3> discord notification </h3>

untuk menggunakan discord notification install terlebih dahulu plugin 

![image](https://user-images.githubusercontent.com/56806850/209431630-2f89eb7b-974a-4d78-8e2c-03ab49ee6b3e.png)

install tanpa merestart jenkins

untuk mengtriggernya tambahkan command pada Jenkinsfile

```shell
post {
    always {
    discordSend description: '', enableArtifactsList: true, footer: '', image: 'https://w7.pngwing.com/pngs/435/546/png-transparent-nico-yazawa-love-live-sunshine-anime-love-live-school-idol-festival-alisa-ayase-anime-child-face-black-hair.png', link: 'https://github.com/KazamiHazaki/Dumbways-FinalTask', result: '', scmWebUrl: '', showChangeset: true, thumbnail: '', title: 'Wayshub-app', webhookURL: 'https://discord.com/api/webhooks/1055488071665188934/yppYX92F1vt_HPuQ6uDFMmCn1PA8MRJ1GeoZuS8TE4CO289bZGT7L2TjDpRiFDCcGFmO'
    }
     }
```
dan sudah berhasil mentrigger notification ke discord

![image](https://user-images.githubusercontent.com/56806850/209431916-e63495be-e48e-4349-b0e7-732aec520935.png)


# <h1> Monitoring </h1>
***

Untuk memonitoring server kita akan menggunakan grafana, prometheus, node exporter.

apa itu grafana ? merupakan aplikasi open-source untuk memvisualisasikan metrics yg di ambil dari prometheus.
lalu apa itu prometheus? merupakan aplikasi untuk mengambil data metrics dari node exporter. 
sedangakan node exporter, merupakan aplikasi untuk mengexpose data metrics ke luar. 

install terlebih dahulu grafana,prometheus, dan node expoterter menggunakan docker compose. 


```shell
version: '3.8'
   
services:
  node-exporter:
    image: bitnami/node-exporter:latest
    container_name: node-exporter
    restart: unless-stopped
    stdin_open: true
    ports:
      - 9100:9100

  prometheus:
    image: bitnami/prometheus:latest
    container_name: prometheus
    restart: unless-stopped
    stdin_open: true
    ports:
      - 9090:9090
    volumes:
      - /home/kel2/grafana/prometheus.yml:/etc/prometheus/prometheus.yml

  grafana:
    image: grafana/grafana
    container_name: grafana
    stdin_open: true
    ports:
      - 3000:3000

```

pada docker compose di atas, volumes prometheus langsung di ambil dari yml prometheus yg sudah di buat dengan isi berikut. 



```shell
global:
  scrape_interval: 15s #mengambil data tiap 15s

scrape_configs:
  - job_name: "prometheus" #nama job yg akan muncul pada grafana
    scrape_interval: 15s #mengambil data tiap 15s
    static_configs:
    - targets: ["185.135.137.176:9090"] # target yg akan di ambil datanya

  - job_name: "node"
    scrape_interval: 15s #mengambil data tiap 15s
    static_configs:
    - targets: ["185.135.137.176:9100"] # target yg akan di ambil datanya

```

jadi ketika docker compose di install, maka prometheus akan secara otomatis menggunakan prometheus yg berada di folder grafana


![image](https://user-images.githubusercontent.com/56806850/207483361-4466d6f2-3af0-4d79-a2da-e56b01acfaf9.png)

lalu setelah membuat docker-compose.yml dan prometheus.yml jalankan docker compose. 


![image](https://user-images.githubusercontent.com/56806850/207483484-90d43a06-77f1-41a3-963b-93635b3560f6.png)

container sudah berjalan dan bisa langsung di buka grafana menggunakan port 3000.

![image](https://user-images.githubusercontent.com/56806850/207483592-cdff3bfc-6dfd-4daf-8184-7ebdc31f11cf.png)


secara default username dan password grafana adalah `admin/admin` 

![image](https://user-images.githubusercontent.com/56806850/207483852-dcbbe606-f51c-4a1c-b994-9a48f62c0c1d.png)

lalu ke configurasi dan tambahkan data source terlebih dahulu

![image](https://user-images.githubusercontent.com/56806850/207484068-1c48ded2-ce45-4f30-8bb2-6da399e86c20.png)

kemudian pilih prometheus 

![image](https://user-images.githubusercontent.com/56806850/207484198-7c4d1b29-8692-4910-962b-e16556717929.png)

setelah menambahkan data source kemudian kita buat dashboard baru 

![image](https://user-images.githubusercontent.com/56806850/207484468-bad521bc-4092-4380-813b-73f0c2715ea5.png)

dan tambahkan panel baru 

![image](https://user-images.githubusercontent.com/56806850/207484678-e72a3913-e728-471a-bd7d-300b2b266349.png)

lalu kita masuk ke edit panel tampilannya akan seperti ini 

![image](https://user-images.githubusercontent.com/56806850/207484727-3179b5c5-faac-4888-bf55-570d19056b81.png)


setelah itu kita buat metrics berdasarkan data dari prometheus.
![image](https://user-images.githubusercontent.com/56806850/207484787-ed5b29c8-c71c-4c4b-bf8b-a2aaf7e7f448.png)

kemudian pilih metrics yg akan di gunakan.

<h3> Import Dashboard Template <h3>
 
 kebagian import dashboard 
 
 ![image](https://user-images.githubusercontent.com/56806850/209434527-83d542ff-a9ba-449b-8473-13d81a3d8f19.png)

 kemudian masukan ID node exporter full 

![image](https://user-images.githubusercontent.com/56806850/209434732-2db7cd8d-1c06-4079-a0a2-c74f5ce8e419.png)

dan load
 
 ![image](https://user-images.githubusercontent.com/56806850/209434791-cb360afe-2a48-4623-bd9e-521ca7f8543f.png)

 lalu import
 
 ![image](https://user-images.githubusercontent.com/56806850/209435090-418fa0c1-df9d-42b2-9dc6-8d19143cb5a2.png)


<h3> Membuat Alert CPU dan RAM usage</h3>

 kemnali ke dashboard kemudian tab alert
 
 ![image](https://user-images.githubusercontent.com/56806850/209435114-cab9c5b5-de17-4ba4-9105-ff541080f60f.png)

 pilih alert lalu buat alert baru
 


***
# <h1> Web Server </h1>
<h2>Install nginx</h2>

```shell
sudo apt update
sudo apt install nginx

```

![image](https://user-images.githubusercontent.com/56806850/209050879-a0ad722f-83cb-4829-b2f9-a9818d5dcb45.png)

kemudian ijinkan firewall NGINX

```shell
sudo ufw app list
sudo ufw allow "Nginx HTTP"
sudo ufw allow "Nginx HTTPS"
sudo ufw allow "Nginx FULL"
sudo ufw enable
```

![image](https://user-images.githubusercontent.com/56806850/209050941-b307ed0b-59f0-408b-829f-6391111ee9d9.png)

setelah itu kita tambahkan reverse proxy, dan edit nginx.conf

`reverse.conf` di simpand pada folder `/etc/nginx/conf.d/`
```shell
server {
    server_name aziz.studentdumbways.my.id ;
    location / {
      proxy_pass http://10.36.116.18:3000/;
 }
}

server {
    server_name api.aziz.studentdumbways.my.id ;
       location / {
      proxy_pass http://10.36.116.18:5000;
 }
}

server {
    server_name prom.aziz.studentdumbways.my.id; 
    location / {
    proxy_pass http://10.36.116.70:9090;
 }
}

server {

    server_name dashboard.aziz.studentdumbways.my.id;
    location / {
    proxy_http_version  1.1;
        proxy_cache_bypass  $http_upgrade;

        proxy_set_header Upgrade           $http_upgrade;
        proxy_set_header Connection        "upgrade";
        proxy_set_header Host              $host;
        proxy_set_header X-Real-IP         $remote_addr;
        proxy_set_header X-Forwarded-For   $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_set_header X-Forwarded-Host  $host;
        proxy_set_header X-Forwarded-Port  $server_port; 
        proxy_pass http://10.36.116.70:3000;

    }
}
```

untuk file nginx.conf hanya di hapus pada bagian # pada `server_names_has_bucket_size`

![image](https://user-images.githubusercontent.com/56806850/209052672-11d1a9ac-89cf-4ee0-af5b-54aa0431fd7b.png)

kemudian save dan test configurasi 
```shell
sudo nginx -t
```
![image](https://user-images.githubusercontent.com/56806850/209052730-6c8fd5e5-0062-4cf1-a898-7c1c37d323ff.png)

<h2> install SSL using Certbot </h2>

update terlebih dahulu snapd jika sudah ada 

```shell
sudo snap install core; sudo snap refresh core
```

jika belum install terlebih dahulu 

```shell
 sudo apt update
 sudo apt install snapd
```

kemudian install certbot, disini akan menggunakan yg versi wildcard

```shell
sudo snap install --classic certbot
```
![image](https://user-images.githubusercontent.com/56806850/209049534-60201b96-96e7-4a71-bc61-acdc3e5e9a2d.png)

untuk memastikan certbot command bisa digunakan jalankan perintah berikut

```shell
sudo ln -s /snap/bin/certbot /usr/bin/certbot
```

lalu jalankan perintah untuk memastikan plugin telah terinstall versi yg sama `classic`

```shell
sudo snap set certbot trust-plugin-with-root=ok
```

dan install DNS plugin, disini menggunakan plugin cloudflarem, untuk DNS provider bisa di cek [disini](https://certbot.eff.org/docs/using.html#dns-plugins)


```shell
sudo snap install certbot-dns-cloudflare
```


![image](https://user-images.githubusercontent.com/56806850/209049906-c6955295-3ad4-49fd-99c6-312d98ab5b2c.png)

lalu kita siap mengisntal SSL karena menggunakan nginx cukup gunakan command 

```shell
sudo certbot --nginx
```
lalu ikuti installasi berikut 

![image](https://user-images.githubusercontent.com/56806850/209050256-66ac13df-aa09-4be7-9e2c-6320406a6c61.png)


setelah installasi ssl seelsai secara otomatis akan berubah menjadi HTTPS setelah di refresh halaman tersebut 

![image](https://user-images.githubusercontent.com/56806850/209050409-96a08f09-1a20-41bc-9424-6e9e47910fc8.png)

a
***
# <h1> Microservices </h1>

Disini microservices akan menggunakan Docker swarm, pertama lakukan Docker swarm init sebagai master docker swarm 

```shell
docker swarm init
```
![image](https://user-images.githubusercontent.com/56806850/209431986-55263bd5-fe8d-4efc-b238-c825f317e618.png)

maka akan muncul join dan token untuk join ke manager docker swarm
```shell
docker swarm join --token SWMTKN-1-2n8dq0c1qyoar0pxy3fo3o17c05lp869rw9slwnv3jfy2u2gk0-bgacsqq25a4xurz00qorc7m8b 154.26.155.62:2377
```

paste pada docker worker

![image](https://user-images.githubusercontent.com/56806850/209432003-83b083b6-ddd4-41c3-8958-ff6dc7c944c0.png)

setelah itu kita bisa mengecek woker di server master
```shell
docker node ls
```

![image](https://user-images.githubusercontent.com/56806850/209432009-49e80900-5b35-43a7-aea2-f3eb37a9b926.png)

kemudian kita deploy menggunakan docker compose berikut 

```yml
version: "3.8"
services:
   mysql_db:
    image: mysql
    container_name: wayshub_mysql_db
    restart: always
    stdin_open: true
    ports:
     - "3306:3306"
    environment:
     - MYSQL_ROOT_PASSWORD=root
     - MYSQL_USER=aziz
     - MYSQL_PASSWORD=Wayshub1
     - MYSQL_DATABASE=wayshub

    volumes:
     - "/home/aziz/database:/var/lib/mysql"
   
   wayshub_be:
    image: kazamisei98/wayshub_be:1.1
    container_name: wayshub_be
    ports:
     - 5000:5000
    depends_on:
     - mysql_db
   
   frontend:
    image: kazamisei98/wayshub_fe:latest
    container_name: wayshub_fe
    ports:
     - 3000:3000
    depends_on:
     - mysql_db

```

gunakan docker stack

```docker
docker stack deploy --compose-file docker-compose.yml wayshub
```
![image](https://user-images.githubusercontent.com/56806850/209432286-f0c277f8-11d3-476c-9ad2-96211209d3ef.png)

lalu cek docker service

```docker 
docker service ls
```

![image](https://user-images.githubusercontent.com/56806850/209432314-f0fe6c0c-807c-4046-91dd-82460eb0b3e7.png)



![image](https://user-images.githubusercontent.com/56806850/209432917-d9cfb48c-e20b-4af1-a5fb-59c23a99b5ea.png)

frontend sudah bisa di akses


setelah itu kita replica frontend menjadi 2

```shell
docker service scale <nama-container>=2
```

![image](https://user-images.githubusercontent.com/56806850/209432855-7366fd66-3ffc-46f6-8c6c-7fd7977e68db.png)


dan frontend berhasil di replica 

![image](https://user-images.githubusercontent.com/56806850/209432869-ca8f8d89-bae5-490b-8d20-998e654624b4.png)





