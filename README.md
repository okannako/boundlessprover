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
- Tmux ekranı açıyoruz çünkü kurulumlar uzun sürüyor server bilgisayarınızla iletişimi uzun bekleyişlerde koparabiliyor bu da kurulumu sonlandırır.
- Kurulumun sırasında bizden cüzdan priv key ve seçtiğimiz ağa göre RPC isteyecek.

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
### Broker Config ayarlarında neler yapmalıyız ve hangi ayar neyi ifade ediyor ?
- Kurulum sonunda ise istediği belirli broker ayarları var bunlara değerler girmemiz gerekiyor. Bu ayarlar her sisteme her kullanıcıya ve ağın o anki durumuna göre değişebilir. O yüzden bireysel bir şekilde ayarlar üzerinde uğraşarak yapmanız gerekiyor. Peki bu ayarların anlamı ne ?  

  1️⃣ mcycle_price > 1 milyon hesaplama döngüsü (cycles) için verdiği fiyat yani bu değeri ne kadar düşük tutarsan diğer tekliflerin önüne geçme ihtimalin daha da artar. Ama değeri çok fazla düşürürsen zarar edersin ya da sistem bu değeri kabul etmez. Burada stabil bir değer çok öenmli.    

  2️⃣ peak_prove_khz > Bu parametre, node’unun ne kadar güçlü bir hesaplama kapasitesine sahip olduğunu Boundless sistemine bildiriyor Yani bu değeri yüksek yazarsak ve sistem karşılayamazsa, order başarısız olur. Düşük yazarsak ise güçlü makinanda potansiyelini kullanamazsın. (Ayrıca scriptte bunu test edebileceğimiz bir seçenek de var. Explorer'den bir orderı alıp ID'sini scriptten Run Benchmark (Order IDs) seçeneğini kullanarak girerseniz sizin kartınıza göre bir değer çıkarıyor. Bunun biraz altını girmeniz yeterli olacaktır.  

  3️⃣ max_mcycle_limit > Bir iş emrinde kabul edilebilecek en fazla hesaplama döngüsü (million cycles = mcycles) sınırını belirleyen bir parametredir. Büyük ve riskli işlerden kaçınarak ceza almaktan korunmuş oluruz. Vereceğimiz değer ne kadar yüksek olursa risk artar.  

  4️⃣ min_deadline > Node'un bir order için deadline’a (son teslim süresine) ne kadar zaman kalmışsa, o işi kabul edip etmeyeceğini belirler. Eğer bu değer düşük olursa işin teslim süresi çok yakın olur ve node order'ı tamalayamaz ise ve ceza yersin. Düşük değer risk yüksek.  

  5️⃣ max_concurrent_proofs = Bu ayar node'un aynı anda kaç tane order kilitleyip işlemeye başlayabileceğini belirtiyor. Yani buradaki değer aynı anda kaç iş almaya çalışabileceğinizi belirtir. Fazlası kartı yorar ve order'ı teslim edemezsin.  

  6️⃣ lockin_priority_gas > Bu değer, senin broker (node) sisteminin bir iş emrini (order) almaya çalışırken ne kadar öncelikli olduğunu belirlemek için fazladan ödeyeceği gas miktarını ifade ediyor. Çok yükseltmek daha rahat lock-in yapmaya yarar ama gereksiz gas harcanmasına nededn olur.    

- ⚠️ Buradaki değerlerin hepsi makina özelliklerinize göre değiştiğinden net bir değer veremiyorum. Ancak alt tarafa 4090 için kullandığım ortalama değerleri yazacağım. Sizde kendi durumunuza göre değerleri girip denemeler yapıp uygun derleri bulabilirsiniz.   
  1️⃣ mcycle_price ="0,0000000000001"  
  2️⃣ peak_prove_khz ="480"  
  3️⃣ max_mcycle_limit ="10000"  
  4️⃣ min_deadline ="60"  
  5️⃣ max_concurrent_proofs ="2" veya "3"  
  6️⃣ lockin_priority_gas = "1000000"

- Explorer Testnet ve Mainnet olarak ikiye ayrıldı. Hangi ağda çalıştırıyorsanız o explorerdan kontrol edebilirsiniz.  
  1️⃣ Testnet Ağları: https://explorer.beboundless.xyz/orders  
  2️⃣ Mainnet Ağı (Base): https://explorer.testnet.beboundless.xyz/orders  

![boundddd](https://github.com/user-attachments/assets/5bbe937d-703b-4dff-a640-4c54ebda6306)

## Ek Kodlar
- İsim vererek tmux ekranı açmak: ````tmux new-session -t boundless````
- Tmux ekranında çıkmak: Önce ````ctrl+b```` sonra ````d```` bas
- Tmux ekranına tekrar giriş yapmak: ````tmux attach -t boundless````
- Tmux ekranlarını listelemek: ````tmux ls````
