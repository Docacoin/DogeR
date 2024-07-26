Instal penjelajah blok di Ubuntu Server 22.04 dengan tutorial berikut.

Perbarui server Ubuntu Anda dengan perintah berikut:

sudo apt-get update && sudo apt-get upgrade -y

Instal dependensi dengan perintah berikut:

sudo apt-get install gnupg2 nodejs npm git nano cmake screen unzip -y

Impor kunci GPG MongoDB:

wget -nc https://www.mongodb.org/static/pgp/server-6.0.asc
cat server-6.0.asc | gpg --dearmor | sudo tee /etc/apt/keyrings/mongodb.gpg >/dev/null

Instal repositori MongoDB dengan perintah berikut:

sudo sh -c 'echo "deb [ arch=amd64,arm64 signed-by=/etc/apt/keyrings/mongodb.gpg] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/6.0 multiverse" >> /etc/apt/sources.list.d/mongo.list'

Perbarui server Ubuntu Anda dengan perintah berikut:

sudo apt-get update -y

Instal MongoDB dengan perintah berikut:

sudo apt install mongodb-org -y

Instal dependensi yang diperlukan dengan perintah berikut:

sudo apt-get install build-essential libminiupnpc-dev libevent-dev libzmq3-dev unzip -y

Unduh Boost dengan perintah berikut:

wget https://boostorg.jfrog.io/artifactory/main/release/1.65.1/source/boost_1_65_1.tar.gz

Ekstrak file tar dengan perintah berikut:

tar -xzvf boost_1_65_1.tar.gz

Instal Boost dengan perintah berikut:

cd boost_1_65_1
./bootstrap.sh --prefix=/usr/local
./b2
sudo ./b2 install

Ketik perintah berikut untuk membuka direktori home Anda:

cd $HOME

Unduh Berkeley DB dengan perintah berikut:

wget http://download.oracle.com/berkeley-db/db-4.8.30.zip

Ekstrak file dengan perintah berikut:

unzip db-4.8.30.zip

Instal Berkeley DB dengan perintah berikut:

cd db-4.8.30
sed -i 's/__atomic_compare_exchange/__atomic_compare_exchange_db/g' dbinc/atomic.h
cd build_unix/
../dist/configure --prefix=/usr/local --enable-cxx
make
sudo make install
export LD_LIBRARY_PATH="$LD_LIBRARY_PATH:/usr/local/lib"

Ketik perintah berikut untuk membuka direktori home Anda:

cd $HOME

Unduh OpenSSL dengan perintah berikut:

wget https://www.openssl.org/source/openssl-1.1.1t.tar.gz

Ekstrak file tar dengan perintah berikut:

tar -xzvf openssl-1.1.1t.tar.gz

Instal OpenSSL dengan perintah berikut:

cd openssl-1.1.1t
./config
make
sudo make install

Buat tautan simbolik dengan perintah berikut:

cd /usr/lib/x86_64-linux-gnu
sudo ln -s libminiupnpc.so /usr/lib/x86_64-linux-gnu/libminiupnpc.so.10
sudo ln -s libevent_pthreads.so /usr/lib/x86_64-linux-gnu/libevent_pthreads-2.1.so.6
sudo ln -s libevent.so /usr/lib/x86_64-linux-gnu/libevent-2.1.so.6

Ketik perintah berikut untuk membuka direktori home Anda:

cd $HOME

Unduh daemon Linux untuk dompet Anda dengan perintah berikut:

wget "https://dl.walletbuilders.com/download?customer=0e5755b446b6d5a92b4b095543549b2ce1a25c80063a72340f&filename=doger-daemon-linux.tar.gz" -O doger-daemon-linux.tar.gz

Ekstrak file tar dengan perintah berikut:

tar -xzvf doger-daemon-linux.tar.gz

Unduh alat Linux untuk dompet Anda dengan perintah berikut:

wget "https://dl.walletbuilders.com/download?customer=0e5755b446b6d5a92b4b095543549b2ce1a25c80063a72340f&filename=doger-qt-linux.tar.gz" -O doger-qt-linux.tar.gz

Ekstrak file tar dengan perintah berikut:

tar -xzvf doger-qt-linux.tar.gz

Ketik perintah berikut untuk menginstal daemon dan alat untuk dompet Anda:

sudo mv dogerd doger-cli doger-tx /usr/bin/

Ketik perintah berikut untuk membuka direktori home Anda:

cd $HOME

Buat direktori data untuk koin Anda dengan perintah berikut:

mkdir $HOME/.doger

Buka nano.

nano $HOME/.doger/doger.conf -t

Tempel teks berikut ke nano.

rpcuser=rpc_doger
rpcpassword=dR2oBQ3K1zYMZQtJFZeAerhWxaJ5Lqeq9J2
rpcallowip=127.0.0.1
listen=1
server=1
txindex=1
daemon=1
addnode=node3.walletbuilders.com

Simpan berkas dengan pintasan papan ketik ctrl+ x.

Ketik perintah berikut untuk memulai daemon Anda:

dogerd

Ketik perintah berikut untuk memulai MongoDB:

sudo systemctl start mongod

Ketik perintah berikut untuk membuka MongoDB:

mongosh

Ketik perintah berikut untuk membuat database MongoDB bernama “explorerdb”:

use explorerdb

Ketik perintah berikut untuk membuat pengguna MongoDB bernama “iquidus”:

db.createUser( { user: "iquidus", pwd: "414uq3EhKDNX76f7DZIMszvHrDMytCnzFevRgtAv", roles: [ "readWrite" ] } )

Ketik perintah berikut untuk menutup MongoDB:

exit

Ketik perintah berikut untuk mengkloning iquidus-explorer:

git clone https://github.com/walletbuilders/explorer.git explorer

Ketik perintah berikut untuk menginstal iquidus-explorer:

cd explorer && npm install --production

Ketik perintah berikut untuk membuat file settings.json:

cp ./settings.json.template ./settings.json

Buka nano.

nano settings.json -t

Ubah nilai berikut dalam file settings.json

judul - “IQUIDUS” -> “DogeR”.

alamat - Ubah nilai “127.0.0.1” dengan alamat IPv4 server Anda.

koin - “Darkcoin” -> “DogeR”.

simbol - “DRK” -> “DGRC”.

kata sandi - “3xp!0reR” -> “414uq3EhKDNX76f7DZIMszvHrDMytCnzFevRgtAv”.

pelabuhan - “9332” -> “18521”.

pengguna - “darkcoinrpc” -> “rpc_doger”.

lulus - 123gfjk3R3pCCVjHtbRde2s5kzdf233sa” -> “dR2oBQ3K1zYMZQtJFZeAerhWxaJ5Lqeq9J2”.

konfirmasi - “40” -> “20”.

api - “benar” -> “salah”.

pasar - “benar” -> “salah”.

twitter - “benar” -> “salah”.

Simpan berkas dengan pintasan papan ketik ctrl+ x.

Ketik perintah berikut untuk membuka sesi layar:

screen

Ketik perintah berikut untuk memulai penjelajah blok Anda:

cd $HOME/explorer
npm start

Tekan pintasan papan ketik ctrl+ a+ duntuk memutuskan sambungan dari sesi layar Anda.

Ketik perintah berikut untuk membuka crontab:

crontab -e

Tekan tombol Page Down pada papan ketik Anda PgDown.

Tempel teks berikut ke crontab.

@reboot dogerd
*/1 * * * * cd $HOME/explorer && /usr/bin/nodejs scripts/sync.js index update > /dev/null 2>&1
*/5 * * * * cd $HOME/explorer && /usr/bin/nodejs scripts/peers.js > /dev/null 2>&1

Simpan crontab dengan pintasan keyboard ctrl+x

Konfirmasikan bahwa Anda ingin menyimpan crontab dengan pintasan keyboard y+enter

Penjelajah blok dapat diakses di http://replace_with_your_ip:3001
