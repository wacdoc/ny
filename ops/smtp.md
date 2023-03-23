# Pangani seva yanu yotumizira makalata a SMTP

## chiyambi

SMTP ikhoza kugula mwachindunji mautumiki kuchokera kwa ogulitsa mitambo, monga:

* [Amazon SES SMTP](https://docs.aws.amazon.com/ses/latest/dg/send-email-smtp.html)
* [Ali cloud imelo push](https://www.alibabacloud.com/help/directmail/latest/three-mail-sending-methods)

Mutha kupanganso seva yanu yamakalata - kutumiza kopanda malire, mtengo wotsika.

Pansipa, tikuwonetsa pang'onopang'ono momwe tingapangire seva yathu yamakalata.

## Kusankhidwa kwa seva

Seva yokhazikika ya SMTP imafuna IP yapagulu yokhala ndi madoko 25, 456, ndi 587 otseguka.

Mitambo ya anthu yomwe imagwiritsidwa ntchito nthawi zambiri yatsekereza madokowa mwachisawawa, ndipo zitha kukhala zotheka kuwatsegula popereka dongosolo lantchito, koma ndizovuta kwambiri.

Ndikupangira kugula kuchokera kwa omwe ali ndi madoko omwe ali otseguka ndikuthandizira kukhazikitsa mayina obwerera.

Apa, ndikupangira [Contabo](https://contabo.com) .

Contabo ndi wothandizira alendo omwe ali ku Munich, Germany, omwe adakhazikitsidwa mu 2003 ndi mitengo yampikisano kwambiri.

Ngati musankha Euro ngati ndalama zogulira, mtengowo udzakhala wotsika mtengo (seva yokhala ndi kukumbukira kwa 8GB ndi ma CPU 4 amawononga pafupifupi 529 yuan pachaka, ndipo ndalama zoyambira zoyambira ndi zaulere kwa chaka chimodzi).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/UoAQkwY.webp)

Mukamayitanitsa, ndemanga `prefer AMD` , ndipo seva yokhala ndi AMD CPU idzachita bwino.

Zotsatirazi, nditenga VPS ya Contabo monga chitsanzo chosonyeza momwe mungapangire seva yanu yamakalata.

## Kusintha kwadongosolo kwa Ubuntu

Makina ogwiritsira ntchito pano ndi Ubuntu 22.04

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/smpIu1F.webp)

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/m7Mwjwr.webp)

Ngati seva pa ssh ikuwonetsa `Welcome to TinyCore 13!` (monga momwe tawonetsera m'chithunzichi), zikutanthauza kuti dongosololi silinakhazikitsidwebe. Chonde chotsani ssh ndikudikirira kwa mphindi zingapo kuti mulowenso.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/-qKACz9.webp)

`Welcome to Ubuntu 22.04.1 LTS` ikuwonekera, kuyambika kwatha, ndipo mutha kupitiliza ndi izi.

### [Mwachidziwitso] Yambitsani malo achitukuko

Sitepe iyi ndi yosankha.

Kuti zitheke, ndidayika kukhazikitsa ndikusintha dongosolo la pulogalamu ya ubuntu mu [github.com/wactax/ops.os/tree/main/ubuntu](https://github.com/wactax/ops.os/tree/main/ubuntu) .

Thamangani lamulo lotsatirali kuti muyike ndikudina kumodzi.

```
bash <(curl -s https://raw.githubusercontent.com/wactax/ops.os/main/ubuntu/boot.sh)
```

Ogwiritsa ntchito achi China, chonde gwiritsani ntchito lamulo ili m'malo mwake, ndipo chilankhulo, nthawi yanthawi, ndi zina zambiri zidzakhazikitsidwa zokha.

```
CN=1 bash <(curl -s https://ghproxy.com/https://raw.githubusercontent.com/wactax/ops.os/main/ubuntu/boot.sh)
```

### Contabo imathandizira IPV6

Yambitsani IPV6 kuti SMTP itha kutumizanso maimelo okhala ndi ma adilesi a IPV6.

Sinthani `/etc/sysctl.conf`

Sinthani kapena kuwonjezera mizere yotsatirayi

```
net.ipv6.conf.all.disable_ipv6 = 0
net.ipv6.conf.default.disable_ipv6 = 0
net.ipv6.conf.lo.disable_ipv6 = 0
```

Tsatirani [phunziroli la contabo: Kuwonjezera kulumikizidwa kwa IPv6 ku seva yanu](https://contabo.com/blog/adding-ipv6-connectivity-to-your-server/)

Sinthani `/etc/netplan/01-netcfg.yaml` , onjezerani mizere ingapo monga momwe tawonetsera pachithunzichi (Contabo VPS file configuration file ili kale ndi mizere iyi, ingowamasulani).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/5MEi41I.webp)

Kenako `netplan apply` kuti masinthidwe osinthidwa ayambe kugwira ntchito.

Kukonzekera kukachita bwino, mutha kugwiritsa ntchito `curl 6.ipw.cn` kuti muwone adilesi ya ipv6 ya netiweki yanu yakunja.

## Phatikizani ma ops osungirako kasinthidwe

```
git clone https://github.com/wactax/ops.soft.git
```

## Pangani satifiketi yaulere ya SSL ya dzina lanu la domain

Kutumiza makalata kumafuna satifiketi ya SSL kuti muyimbe ndi kusaina.

Timagwiritsa ntchito [acme.sh](https://github.com/acmesh-official/acme.sh) kupanga satifiketi.

acme.sh ndi chida chotsegulira gwero losaina satifiketi,

Lowetsani kasinthidwe warehouse ops.soft, thamangani `./ssl.sh` , ndipo chikwatu cha `conf` chidzapangidwa **m'ndandanda wapamwamba** .

Pezani wopereka wanu wa DNS kuchokera ku [acme.sh dnsapi](https://github.com/acmesh-official/acme.sh/wiki/dnsapi) , sinthani `conf/conf.sh` .

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/Qjq1C1i.webp)

Kenako thamangani `./ssl.sh 123.com` kuti mupange `123.com` ndi `*.123.com` satifiketi za dzina lanu.

Kuthamanga koyamba kumangoyika [acme.sh](https://github.com/acmesh-official/acme.sh) ndikuwonjezera ntchito yomwe idakonzedwa kuti ikonzenso. Mutha kuwona `crontab -l` , pali mzere wotere motere.

```
52 0 * * * "/mnt/www/.acme.sh"/acme.sh --cron --home "/mnt/www/.acme.sh" > /dev/null
```

Njira ya satifiketi yopangidwa ndi chinthu chonga `/mnt/www/.acme.sh/123.com_ecc。`

Kukonzanso kwa satifiketi kudzayitanitsa `conf/reload/123.com.sh` script, sinthani script iyi, mutha kuwonjezera malamulo monga `nginx -s reload` kuti mutsitsimutsenso chinsinsi cha mapulogalamu ogwirizana.

## Pangani seva ya SMTP ndi chasquid

[chasquid](https://github.com/albertito/chasquid) ndi seva yotseguka ya SMTP yolembedwa muchilankhulo cha Go.

Monga cholowa m'malo mwa mapulogalamu akale a seva yamakalata monga Postfix ndi Sendmail, chasquid ndi yosavuta komanso yosavuta kugwiritsa ntchito, komanso ndiyosavuta pakukula kwachiwiri.

Thamangani `./chasquid/init.sh 123.com` idzakhazikitsidwa yokha ndikudina kamodzi (m'malo mwa 123.com ndi dzina lanu lotumizira).

## Konzani Siginecha ya Imelo DKIM

DKIM imagwiritsidwa ntchito potumiza siginecha za imelo kuletsa makalata kuwonedwa ngati sipamu.

Lamulo likayenda bwino, mudzapemphedwa kuti muyike mbiri ya DKIM (monga momwe tawonetsera pansipa).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/LJWGsmI.webp)

Ingowonjezerani mbiri ya TXT ku DNS yanu (monga momwe tawonetsera pansipa).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/0szKWqV.webp)

## Onani mawonekedwe a ntchito & zolemba

 `systemctl status chasquid` Onani mawonekedwe a service.

Mkhalidwe wa ntchito yabwino ndi monga momwe zilili m'chithunzichi

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/CAwyY4E.webp)

 `grep chasquid /var/log/syslog` kapena `journalctl -xeu chasquid` akhoza kuwona chipika cholakwika.

## Kusintha kwa dzina la domain

Reverse domain name ndikulola kuti adilesi ya IP ithetsedwe ku dzina lofananira.

Kuyika dzina loyang'ana kumbuyo kungalepheretse maimelo kudziwika ngati sipamu.

Imelo ikalandiridwa, seva yolandirayo ipanga kusanthula kwa dzina la domain reverse pa adilesi ya IP ya seva yotumiza kuti itsimikizire ngati seva yotumizayo ili ndi dzina loyang'ana kumbuyo.

Ngati seva yotumizayo ilibe dzina loyang'ana kumbuyo kapena ngati dzina loyang'ana kumbuyo silikugwirizana ndi adilesi ya IP ya seva yotumiza, seva yolandila ikhoza kuzindikira imeloyo ngati sipamu kapena kuyikana.

Pitani ku [https://my.contabo.com/rdns](https://my.contabo.com/rdns) ndikukonzekera monga momwe zilili pansipa

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/IIPdBk_.webp)

Mutatha kuyika dzina loyang'ana kumbuyo, kumbukirani kukonza kusamvana kwa dzina la domain ipv4 ndi ipv6 ku seva.

## Sinthani dzina la homuweki wa chasquid.conf

Sinthani `conf/chasquid/chasquid.conf` ku mtengo wa dzina lachibwezi.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/6Fw4SQi.webp)

Kenako thamangani `systemctl restart chasquid` kuti muyambitsenso ntchito.

## Sungani conf ku git repository

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/Fier9uv.webp)

Mwachitsanzo, ndimasunga chikwatu cha conf ku ndondomeko yanga ya github motere

Pangani nyumba yosungiramo zinthu zachinsinsi

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/ZSCT1t1.webp)

Lowetsani chikwatu cha conf ndikutumiza ku nyumba yosungiramo zinthu

```
git init
git add .
git commit -m "init"
git branch -M main
git remote add origin git@github.com:wac-tax-key/conf.git
git push -u origin main
```

## Onjezani wotumiza

thamanga

```
chasquid-util user-add i@wac.tax
```

Mutha kuwonjezera wotumiza

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/khHjLof.webp)

### Tsimikizirani kuti mawu achinsinsi adayikidwa bwino

```
chasquid-util authenticate i@wac.tax --password=xxxxxxx
```

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/e92JHXq.webp)

Pambuyo powonjezera wogwiritsa ntchito, `chasquid/domains/wac.tax/users` zidzasinthidwa, kumbukirani kuzipereka ku nyumba yosungiramo katundu.

## DNS onjezani mbiri ya SPF

SPF (Sender Policy Framework) ndiukadaulo wotsimikizira maimelo omwe amagwiritsidwa ntchito poletsa chinyengo cha imelo.

Imatsimikizira kuti wotumiza makalata ndi ndani poyang'ana kuti adilesi ya IP ya wotumizayo ikugwirizana ndi zolemba za DNS za dzina lachidziwitso lomwe amadzinenera kuti ndi, kuletsa achinyengo kutumiza maimelo abodza.

Kuwonjezera zolemba za SPF kumatha kuletsa maimelo kuti asadziwike ngati sipamu momwe angathere.

Ngati seva yanu ya dzina la domain sigwirizana ndi mtundu wa SPF, ingowonjezerani mbiri yamtundu wa TXT.

Mwachitsanzo, SPF ya `wac.tax` ili motere

`v=spf1 a mx include:_spf.wac.tax include:_spf.google.com ~all`

SPF ya `_spf.wac.tax`

`v=spf1 a:smtp.wac.tax ~all`

Zindikirani kuti `include:_spf.google.com` apa, chifukwa ndikonza `i@wac.tax` ngati adilesi yotumizira mubokosi la makalata la Google pambuyo pake.

## DNS kasinthidwe DMARC

DMARC ndiye chidule cha (Domain-based Message Authentication, Reporting & Conformance).

Amagwiritsidwa ntchito kujambula kuphulika kwa SPF (mwina chifukwa cha zolakwika za kasinthidwe, kapena wina akunamizira kuti ndiwe kutumiza sipamu).

Onjezani mbiri ya TXT `_dmarc` ,

Zomwe zili ndi izi

```
v=DMARC1; p=quarantine; fo=1; ruf=mailto:ruf@wac.tax; rua=mailto:rua@wac.tax
```

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/k44P7O3.webp)

Tanthauzo la parameter iliyonse ili motere

### p (ndondomeko)

Imawonetsa momwe mungagwirire maimelo omwe akulephera kutsimikizira za SPF (Sender Policy Framework) kapena DKIM (DomainKeys Identified Mail). P parameter ikhoza kukhazikitsidwa ku chimodzi mwazinthu zitatu:

* palibe: Palibe chomwe chingachitike, zotsatira zotsimikizira zokha ndizomwe zimabwezeredwa kwa wotumiza kudzera pamakina ofotokozera maimelo.
* Kukhala kwaokha: Ikani makalata omwe sanadutse chitsimikiziro mu foda ya sipamu, koma sangakane makalatawo mwachindunji.
* kukana: Kanani mwachindunji maimelo omwe akulephera kutsimikizira.

### fo (Zosankha Zolephera)

Imatchula kuchuluka kwa zomwe zabwezedwa ndi njira yochitira lipoti. Ikhoza kukhazikitsidwa ku chimodzi mwazinthu zotsatirazi:

* 0: Nenani zotsatira zotsimikizira za mauthenga onse
* 1: Ingonenani mauthenga omwe akulephera kutsimikizira
* d: Ingofotokozani zolephera zotsimikizira dzina la domain
* s: fotokozani zolephera zotsimikizira za SPF
* l: Ingonenani zolephera zotsimikizira za DKIM

### chuma & ruf

* rua (Kupereka Malipoti a URI kwa Malipoti Ophatikiza): Imelo adilesi yolandila malipoti ophatikizidwa
* ruf (Kunena URI kwa malipoti a Forensic): imelo adilesi kuti mulandire malipoti atsatanetsatane

## Onjezani zolemba za MX kuti mutumize maimelo ku Google Mail

Chifukwa sindinapeze bokosi lamakalata laulere lomwe limathandizira maadiresi onse (Catch-All, angalandire maimelo aliwonse otumizidwa ku dzina lachidziwitso ichi, popanda zoletsa pa prefixes), ndinagwiritsa ntchito chasquid kutumiza maimelo onse ku bokosi langa la makalata la Gmail.

**Ngati muli ndi bokosi lanu lamakalata labizinesi yolipira, chonde musasinthe MX ndikudumpha izi.**

Sinthani `conf/chasquid/domains/wac.tax/aliases` , konzani makalata otumizira

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/OBDl2gw.webp)

`*` ikuwonetsa maimelo onse, `i` ndiye choyambira cha imelo cha wotumiza wopangidwa pamwambapa. Kuti atumize maimelo, wogwiritsa ntchito aliyense ayenera kuwonjezera mzere.

Kenako onjezani mbiri ya MX (ndikuloza mwachindunji ku adilesi ya reverse domain name apa, monga momwe zasonyezedwera pamzere woyamba pachithunzichi pansipa).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/7__KrU8.webp)

Zokonza zikatha, mutha kugwiritsa ntchito ma adilesi ena a imelo kutumiza maimelo ku `i@wac.tax` ndi `any123@wac.tax` kuti muwone ngati mungalandire maimelo mu Gmail.

Ngati sichoncho, yang'anani chipika cha chasquid ( `grep chasquid /var/log/syslog` ).

## Tumizani imelo ku i@wac.tax ndi Google Mail

Google Mail italandira imeloyo, mwachibadwa ndimafuna kuyankha ndi `i@wac.tax` m'malo mwa i.wac.tax@gmail.com.

Pitani ku [https://mail.google.com/mail/u/1/#settings/accounts](https://mail.google.com/mail/u/1/#settings/accounts) ndikudina "Onjezani imelo adilesi ina".

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/PAvyE3C.webp)

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/_OgLsPT.webp)

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/XIUf6Dc.webp)

Kenako, lowetsani nambala yotsimikizira yomwe idalandiridwa ndi imelo yomwe idatumizidwako.

Pomaliza, ikhoza kukhazikitsidwa ngati adilesi yotumiza (pamodzi ndi mwayi woyankha ndi adilesi yomweyo).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/a95dO60.webp)

Mwanjira imeneyi, tatsiriza kukhazikitsa seva yamakalata a SMTP ndipo nthawi yomweyo timagwiritsa ntchito Google Mail kutumiza ndi kulandira maimelo.

## Tumizani imelo yoyesa kuti muwone ngati kasinthidweyo akuyenda bwino

Lowani `ops/chasquid`

Thamangani `direnv allow` kuyika zodalira (direnv idayikidwa munjira yoyambira ya kiyi imodzi ndipo mbedza yawonjezedwa ku chipolopolo)

ndiye thamangani

```
user=i@wac.tax pass=xxxx to=iuser.link@gmail.com ./sendmail.coffee
```

Tanthauzo la magawowa ndi motere

* wosuta: SMTP lolowera
* pass: SMTP password
* ku: wolandira

Mutha kutumiza imelo yoyeserera.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/ae1iWyM.webp)

Ndikofunikira kugwiritsa ntchito Gmail kuti mulandire maimelo oyesa kuti muwone ngati zosinthazo zapambana.

### TLS standard encryption

Monga momwe tawonetsera pachithunzichi, pali loko yaying'ono, zomwe zikutanthauza kuti satifiketi ya SSL yathandizidwa bwino.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/SrdbAwh.webp)

Kenako dinani "Show Original Imelo"

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/qQQsdxg.webp)

### DKIM

Monga tawonetsera pachithunzichi, tsamba loyambirira la Gmail likuwonetsa DKIM, zomwe zikutanthauza kuti kasinthidwe ka DKIM ndi kopambana.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/an6aXK6.webp)

Yang'anani Zomwe Zalandilidwa pamutu wa imelo yoyambirira, ndipo mutha kuwona kuti adilesi yotumiza ndi IPV6, zomwe zikutanthauza kuti IPV6 nayonso idakonzedwa bwino.
