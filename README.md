<p align="center">
  <a href="">
    <img alt="Hero" src="https://github.com/user-attachments/assets/6f10e96d-36e7-4cb0-88c2-26d84d8e2739" width="75%" />
  </a>
</p>

## Ön Bilgi
- Boundless, sıfır bilgi kanıtları ZK teknolojisini geliştiricilere ve projelere daha erişilebilir kılmayı amaçlayan bir altyapı protokolüdür.
- Ödüllü testnet Temmuz ayı içinde başlayacak. Ne kadar uzun olacağı belli değil.
- Ekran kartı olan vps'lere kurulum yapılması gerekiyor. Öneri olarak minimum Nvidia RTX 3090 öneriliyor. (Bireysel olarak 3060 deniyorum)

## Tavsiye Edilen Sistem Gereksinimleri
- CPU: 16+ Cores
- RAM: 32+ GB
- SSD: 120+ GB
- Ekran Kartı: VRAM > 8GB - Min: Nvidia Rtx 3090
- İşletim Sistemi: UBUNTU 22.04LTS

## Yükleme Adımları
- Vps üzerinde yükleme adımlarına geçmeden önce almamız gereken faucetler var. Base Mainnet işlemler için pahallı olacağından onrada kurulum yapmayacağım. Test ağları olan Base Sepoli ve Eth Sepolia ağlarında olacak. Hangisini çalıştırmak istiyorsanız o ağda faucetleri almalısınız. İşlemler aynı sadece ağlar farklı.
- Öncelikle testte kullanamak için bir cüzdana ihtiyacımız var. Eğer role alırken kullandığınız varsa o da olur. Ya da tekrar oluşturabilirsiniz. AMA kesinlikle mainnet, airdrop vs için kullandığınız bir cüzdanla giriş yapmayın. Test olduğu ve priv. key kullandığımız için güvenli olmayabilir.
- İlk olarak hangi ağda kurulum yapacaksanız o ağa şuradan USDC fauceti alın > https://faucet.circle.com/
- Daha sonra yine aynı ağa Test Eth alın. Ben her ihtimale karşı 30 adet atmıştım. Karar sizin. Buradan ücreti alıyorsunuz ücretsiz bulduysanız sorun yok. > https://testnetbridge.com/sepolia
- Eğer Base Sepolia'ya ETH geçirecekseniz şu bridge kullanabilirsiniz. > https://superbridge.app/base-sepolia
- Ekran kartlı bir vps kiralamamız lazım. Ben Vast.ai > https://cloud.vast.ai/?ref_id=271399 kulllanıyorum, videoda bunun üzerinden olacak. Tıklayarak üyelik açabilirsiniz.
- Son olarak da blockpi.io üzerinden ücretsiz RPC alıyoruz. Hangi ağda kurulum yaptıysanız o ağdaki alın. Teşvikli testnet sırasında ücretsizler etkisi kalabilir, aynı yerden ücretliye dönmek gerekebilir.
- Artık yükleme adımlarına geçip kurulumu yapabiliriz.

- Kendim bir script ayarlıyacaktım fakat 0xMoei ayrıntılı bir script ayarlamış. Onun üzerinden kurulum yapmak zaman kazanmak açısından daha iyi oldu. Hem burada yazacaklarım hem de videoda anlatacaklarım onun üzerinden olacak. Bir nevi Türkçeye çevrilmesi diyebiliriz. İlk olarak kiraladığımız makinaya bağlanıyoruz.
- Tmux ekranı açıyoruz çünkü kurulumlar uzun sürüyor server bilgisayarınızla iletişimi uzun bekleyişlerde koparabiliyor bu da kurulumu sonlandırır
```
apt install tmux
tmux new-session -t boundless
```
- Tmux ekranı açtıktan aşağıdaki kodlarla devam ediyoruz.
```
# Update packages
apt update && apt upgrade -y

# download wget
apt install wget

# Download the installation script
wget https://raw.githubusercontent.com/0xmoei/boundless/main/install_prover.sh -O install_prover.sh

# Make it executable
chmod +x install_prover.sh

# Run the installer
./install_prover.sh
```

- Dashboard ekranına tekrar ulaşmak.
```
cd ~/boundless
./prover.sh
```
![boundddd](https://github.com/user-attachments/assets/5bbe937d-703b-4dff-a640-4c54ebda6306)

## Broker Config ayarlarında neler yapmalıyız ve hangi ayar neyi ifade ediyor ?

## Dashboard'da ki seçenekler ne işe yarıyor _


## Ek Kodlar
- İsim vererek tmux ekranı açmak: ````tmux new-session -t boundless````
- Tmux ekranında çıkmak: Önce ````ctrl+b```` sonra ````d```` bas
- Tmux ekranına tekrar giriş yapmak: ````tmux attach -t boundless````
- Tmux ekranlarını listelemek: ````tmux ls````
