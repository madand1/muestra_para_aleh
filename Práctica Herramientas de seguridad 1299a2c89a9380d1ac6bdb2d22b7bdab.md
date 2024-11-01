# Práctica Herramientas de seguridad

# Responsabilidad individual

# Alejandro Herrera - Alumno 1

# Raúl Herrera - Alumno 2

## SNORT

### **Introducción**

Documentación del uso y funcionamiento del sistema de detección de intrusos Snort. Incluiremos información exhaustiva de todas las opciones de configuración de alertas.

### **Instalación de la herramienta snort en debian12 en la versión 2.9**

La herramienta SNORT tiene muchas dependencias, lo primero que haremos será instalarnos todas estas dependencias.

```html
**sudo apt-get install flex bison build-essential checkinstall libpcap-dev libnet1-dev libpcre3-dev libnetfilter-queue-dev libxtables-dev libdumbnet-dev zlib1g-dev -y**
```

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXf-27eVCUKg5-8oE7mZuA1AivyXjtcmbQy0nft1RXz4hQaRLjl45DFAtFY_Pl9dl_U4g7iZBFpV8OkZCtJ6RbjzIoAzcRerVnxJL2OHTMhC7E2-vptEYywx1Pj7Kl4kMKfMVbOMF_EZiRETZNLFfSPmxVWr?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf-27eVCUKg5-8oE7mZuA1AivyXjtcmbQy0nft1RXz4hQaRLjl45DFAtFY_Pl9dl_U4g7iZBFpV8OkZCtJ6RbjzIoAzcRerVnxJL2OHTMhC7E2-vptEYywx1Pj7Kl4kMKfMVbOMF_EZiRETZNLFfSPmxVWr?key=REBS4JzpPJr9JzQsSLcUIg)

Una vez instaladas las dependencias, debemos instalar el Data Acquisition Library

**`wget https://www.snort.org/downloads/snort/daq-2.0.7.tar.gz`**

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXe6sJ-A9ncRx9VytJpeGshjQt75EOppnogWv9QkLmHz37xlwrow_Fg3patHQX8vc8WGZDMNhKpg2zsSvwWsw69ioHwxMrsCV3iecy-2_7V5LXNcc-R36dvFAUl-L6CTRCeAElcG2oUnw1AdkFnFZmSxBq7u?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXe6sJ-A9ncRx9VytJpeGshjQt75EOppnogWv9QkLmHz37xlwrow_Fg3patHQX8vc8WGZDMNhKpg2zsSvwWsw69ioHwxMrsCV3iecy-2_7V5LXNcc-R36dvFAUl-L6CTRCeAElcG2oUnw1AdkFnFZmSxBq7u?key=REBS4JzpPJr9JzQsSLcUIg)

**`sudo tar -xvzf daq-2.0.7.tar.gz`**

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXcW7vMlL2CDXtq27BV1WUnbFtq296nlUWC9FnvW-e6K_EA0xeqV_UNqkw-mfqqGI08EXY02q8Hy1Jb_6zd8vOk1AgmL_Wu802vBjyo0zm8rUx213I8YOMOlbbUmYPs4rmHg5gAZVogyyukYe3jUpSiYWII?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcW7vMlL2CDXtq27BV1WUnbFtq296nlUWC9FnvW-e6K_EA0xeqV_UNqkw-mfqqGI08EXY02q8Hy1Jb_6zd8vOk1AgmL_Wu802vBjyo0zm8rUx213I8YOMOlbbUmYPs4rmHg5gAZVogyyukYe3jUpSiYWII?key=REBS4JzpPJr9JzQsSLcUIg)

Y lo instalamos desde las dependencias con

**`sudo ./configure, sudo make, sudo make install`**

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXc1-95MvF1GPDuyFiHXESD-fPDqGCKSzVKabjwvJryjMsooL-qP5kGT84LrxRx5nVqCLEnvF4QgAfXFfsdQ3BDqC70h_16bNzI1FbKOLDRR4OQAAR-I9QxrsfVqtehXF956UlejPp08ozTzlOvfbew-_mn5?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXc1-95MvF1GPDuyFiHXESD-fPDqGCKSzVKabjwvJryjMsooL-qP5kGT84LrxRx5nVqCLEnvF4QgAfXFfsdQ3BDqC70h_16bNzI1FbKOLDRR4OQAAR-I9QxrsfVqtehXF956UlejPp08ozTzlOvfbew-_mn5?key=REBS4JzpPJr9JzQsSLcUIg)

Vemos que ya se ha instalado daq, ya tenemos dicha librería. Ahora pasamos a instalar **SNORT**

```html
**sudo wget https://www.snort.org/downloads/snort/snort-2.9.20.tar.gz
sudo tar -xvzf snort-2.9.20.tar.gz
cd snort-2.9.20
sudo ./configure
sudo make
sudo make install**
```

Al hacer `sudo ./config` nos da el siguiente error:

> ERROR!  LuaJIT library not found. Go get it from http://www.luajit.org/ (or)
Try compiling without openAppId using '--disable-open-appid'
configure: error: "Fatal!"
> 

Para solucionarlos nos tendremos que instalar el siguiente binario: `**sudo apt install libluajit-5.1-dev -y**`

Al hacer **`sudo make`** me da el siguiente error:

```html
sp_rpc_check.c:32:10: fatal error: rpc/rpc.h: No existe el fichero o el directorio 32 | #include <rpc/rpc.h> | ^~~~~~~~~~~ compilation terminated.
```

Se supone que instalando las siguientes dependencias: **`sudo apt install libntirpc-dev`**

Debería dejarnos, pero en mi caso no me deja. Lo que he tenido que hacer es lo siguiente:

Clonar el siguiente repositorio de github: **`sudo git clone [https://github.com/lattera/glibc.git](https://github.com/lattera/glibc.git)`**

Mover todos los archivos de la carpeta del repositorio a la siguiente en nuestro local:

**`sudo cp -avr glibc/sunrpc/rpc/* /usr/include/rpc`**

Y una vez hecho esto ya podemos hacer el **`sudo make && sudo make install`**

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXczpm3I9deHiQ-NB4KoPgVYK3YK41Vum8LwE4C1s9_6vyKfACc6G2j_DrHXgCNJhQcKF2E9dMBTGHlz6frK5d9XkWi9k0r8HsToDWs6IQHBnI6qimiV8acF5k6PykNb4xEkfmNe8UadFEVBzpQ0Mf4EqdYM?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXczpm3I9deHiQ-NB4KoPgVYK3YK41Vum8LwE4C1s9_6vyKfACc6G2j_DrHXgCNJhQcKF2E9dMBTGHlz6frK5d9XkWi9k0r8HsToDWs6IQHBnI6qimiV8acF5k6PykNb4xEkfmNe8UadFEVBzpQ0Mf4EqdYM?key=REBS4JzpPJr9JzQsSLcUIg)

Como observamos ya lo tenemos instalado y bien configurada la librería daq.

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXdSHQYd0RfBiy-Fk7XACO6ag2ekcvSZp0PFgGWE4z14F974D4LcsnrY8rLrWnZ-z6K85bYlEYaDmBBxELbHUOe1t4OFDV_Bui8Tsxd_J7NrHVmlB2beG7p4KRzZgwIslFYU5fp_hMwHn7TuccsnfF78V75j?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdSHQYd0RfBiy-Fk7XACO6ag2ekcvSZp0PFgGWE4z14F974D4LcsnrY8rLrWnZ-z6K85bYlEYaDmBBxELbHUOe1t4OFDV_Bui8Tsxd_J7NrHVmlB2beG7p4KRzZgwIslFYU5fp_hMwHn7TuccsnfF78V75j?key=REBS4JzpPJr9JzQsSLcUIg)

> **Todo lo realizado anteriormente no funciona porque hay un error con snort 2.9 en debian y no lee bien las reglas, por lo que pasamos a instalar snort 3. Con esto también nos surge un nuevo problema, necesitamos un Daq más actualizado para que funcione con Snort3. Para ello he creado una nueva MV para que la configuración de la antigua no interrumpa en el nuevo Snort.**
> 

**Los pasos son los mismos, van a ser un poco más resumidos en esta parte:**

### **Instalación de la herramienta snort en debian12 en la versión 3.1**

```html
**Instalamos pre requisitos:** **sudo apt install build-essential libpcap-dev libpcre3-dev libnet1-dev zlib1g-dev luajit hwloc libdumbnet-dev bison flex liblzma-dev openssl libssl-dev pkg-config libhwloc-dev cmake cpputest libsqlite3-dev uuid-dev libcmocka-dev libnetfilter-queue-dev libmnl-dev autotools-dev libluajit-5.1-dev libunwind-dev libfl-dev -y**
```

Ya tenemos el primer problema, no se puede localizar el paquete **libdnet-dev**. Buscando nos damos cuenta que dicho paquete estaba en Debian buster (oldoldstable). Al saber que ha estado en otra distribución de debian lo único que tenemos que hacer es añadir el repositorio de dicha distribución en el `/etc/apt/sources.list` y hacer un `update e install.`

**`sudo nano /etc/apt/sources.list`**

Añadimos:

`deb http://deb.debian.org/debian/ buster main non-free-firmware`

**`sudo apt update && sudo apt install libdnet-dev`**

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXft32x81lp91w-qE1mX6gmLhrclGGu-5Lc-XGw7eNKFx0oQIU8MEQcn2ihgsGRAoSYm2cHhCBOn0pongmSlywWFjhfeVsqoESkpPN4K1RP47-Q-HZgyRTZpr-Px7IvwXq8afUWWXwZBDk7nZB8VSc_qMjA?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXft32x81lp91w-qE1mX6gmLhrclGGu-5Lc-XGw7eNKFx0oQIU8MEQcn2ihgsGRAoSYm2cHhCBOn0pongmSlywWFjhfeVsqoESkpPN4K1RP47-Q-HZgyRTZpr-Px7IvwXq8afUWWXwZBDk7nZB8VSc_qMjA?key=REBS4JzpPJr9JzQsSLcUIg)

**`cd && sudo mkdir snort && cd snort`**

**Instalación de Daq:**

```html
**sudo git clone [https://github.com/snort3/libdaq.git](https://github.com/snort3/libdaq.git)
cd libdaq/
sudo ./bootstrap**
```

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXdIQUZLqXA9qrjAnUHApwoIMtem5GYZqhGVzP665VF644uIAl5rKQ2k76X3x9LJdYoOFMvVixXwXYstngOsp2WxQYI-DiOvTOit8pfFmOHq_OddeYz9KdpwETGq067awPXbYYy2Ps_aJ929epHGOO0GCvU?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdIQUZLqXA9qrjAnUHApwoIMtem5GYZqhGVzP665VF644uIAl5rKQ2k76X3x9LJdYoOFMvVixXwXYstngOsp2WxQYI-DiOvTOit8pfFmOHq_OddeYz9KdpwETGq067awPXbYYy2Ps_aJ929epHGOO0GCvU?key=REBS4JzpPJr9JzQsSLcUIg)

```html
**sudo ./configure
sudo make
sudo make install**
```

Me lo ha ejecutado todo sin ningún error.

**Instalación de Gperftools:**

Para snort3 necesitamos la **última versión** de **Gperftools**, para ello haremos lo siguiente:

```html
**cd ..
sudo wget https://github.com/gperftools/gperftools/releases/download/gperftools-2.9.1/gperftools-2.9.1.tar.gz
sudo tar xzf gperftools-2.9.1.tar.gz
cd gperftools-2.9.1/
sudo ./configure
sudo make
sudo make install**
```

Se ha instalado todo sin ningún error.

**Instalación de Snort3:**

```html
**cd ..
sudo wget [https://github.com/snort3/snort3/archive/refs/tags/3.1.43.0.tar.gz](https://github.com/snort3/snort3/archive/refs/tags/3.1.43.0.tar.gz)
sudo tar -xvzf 3.1.43.0.tar.gz
cd snort3-3.1.43.0/
sudo ./configure_cmake.sh --prefix=/usr/local --enable-tcmalloc
sudo cd build
sudo make
sudo make install
sudo ldconfig**
```

Se ha ejecutado todo sin darme ningún fallo.

Ahora debemos añadir al **.bashrc** la siguiente línea: **`export PATH=$PATH:/usr/local/bin`**

Y ya tenemos **snort en su versión 3**:

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXf9az1UmlA-JqzhRRf1UFdgu_KJ-_r1Z_qo_a4e_sEd5LRWgARm0Mgq8EGq-7THUHpjohdb62Py2kkbxv4cdP91MiKSUN6uz5kNXy1r236mR_1PktWRnql-wVNTv8vC_BNMLv_fXVXW73PldO9v_laZe55-?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf9az1UmlA-JqzhRRf1UFdgu_KJ-_r1Z_qo_a4e_sEd5LRWgARm0Mgq8EGq-7THUHpjohdb62Py2kkbxv4cdP91MiKSUN6uz5kNXy1r236mR_1PktWRnql-wVNTv8vC_BNMLv_fXVXW73PldO9v_laZe55-?key=REBS4JzpPJr9JzQsSLcUIg)

### **Configuración de la herramienta Snort en Debian12**

En primer lugar, configuramos la interfaz de red en modo promiscuo para que pueda ver todo el tráfico de la red, lo haremos con el siguiente comando:

**`sudo ip link set dev enp1s0 promisc on`**

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXcCy6uKl8joQsY-DmpP6qCMbW24Cm3jkGE4k8q6z7RCA3lk8XrVDKUYBCEO8e0X2mYV73idVEbKlVYANAa_qex1IimwTuSJLMACju6oK6mzauJy_uGZaMjFmn8YDQ9_9yIbC_od7Zlcea0c1AzBzTYbebc?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcCy6uKl8joQsY-DmpP6qCMbW24Cm3jkGE4k8q6z7RCA3lk8XrVDKUYBCEO8e0X2mYV73idVEbKlVYANAa_qex1IimwTuSJLMACju6oK6mzauJy_uGZaMjFmn8YDQ9_9yIbC_od7Zlcea0c1AzBzTYbebc?key=REBS4JzpPJr9JzQsSLcUIg)

A continuación, también tenemos que desactivar la descarga de la interfaz, así nos aseguramos que la interfaz de red siga activa. En primer lugar, comprueba si esta función está activada o no mediante el siguiente comando:

**`sudo apt install ethtool -y`**

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXdC5dDe-hRksHLrGUlWvoUWJAGgAyw4EKML0Wor8YRaCyXdijmkLSdDzn11drA27ne-vo5ec4b_wlqf5nrFEQNdjKuPVEO0kCf7UBRZeUPX9qSKitJAjFUREOMbiVp01dUrBZJpdemy-tx8Fqjd4KpxL8Ht?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdC5dDe-hRksHLrGUlWvoUWJAGgAyw4EKML0Wor8YRaCyXdijmkLSdDzn11drA27ne-vo5ec4b_wlqf5nrFEQNdjKuPVEO0kCf7UBRZeUPX9qSKitJAjFUREOMbiVp01dUrBZJpdemy-tx8Fqjd4KpxL8Ht?key=REBS4JzpPJr9JzQsSLcUIg)

**`sudo ethtool -k enp1s0 | grep receive-offload`** 

Obtendremos lo siguiente:

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXcIsGfXqPaC9pqm_nOHogu44IoFexQMSYeEKleVJP9eOAB07kmd1r2jAKA3cHfEP1R10_BK9ee2ML_QGiwcIpzNVAWd6dV9gXpMv-_46QFlv1V3jdfQrED67qJsgpASDuIPhwQK4NnocPostRFgANgLR94C?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcIsGfXqPaC9pqm_nOHogu44IoFexQMSYeEKleVJP9eOAB07kmd1r2jAKA3cHfEP1R10_BK9ee2ML_QGiwcIpzNVAWd6dV9gXpMv-_46QFlv1V3jdfQrED67qJsgpASDuIPhwQK4NnocPostRFgANgLR94C?key=REBS4JzpPJr9JzQsSLcUIg)

Lo desactivamos con el siguiente comando:

**`sudo ethtool -K enp1s0 gro off lro off`**

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXdPnnJgo0Oh-80LvnE9WuSiS4N8JAChNJKYu1cuNxljanZLDxPPgDYAgwuM3sNb4DnFRJuAaA9l55dHHksvm6K_YNKpvgbxu397Q6McOClJjq4f0wmmWlgw1xyT2jyi2I70fHTUMxDr8e-wmdzyy43E4ic2?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdPnnJgo0Oh-80LvnE9WuSiS4N8JAChNJKYu1cuNxljanZLDxPPgDYAgwuM3sNb4DnFRJuAaA9l55dHHksvm6K_YNKpvgbxu397Q6McOClJjq4f0wmmWlgw1xyT2jyi2I70fHTUMxDr8e-wmdzyy43E4ic2?key=REBS4JzpPJr9JzQsSLcUIg)

A continuación, creamos un archivo de servicio systemd para Snort NIC.

**`sudo nano /etc/systemd/system/snort3-nic.service`**

Añadimos las siguientes líneas:

```html
[Unit]
Description=Set Snort 3 NIC in promiscuous mode and Disable GRO, LRO on boot
After=network.target
[Service]
Type=oneshot
ExecStart=/usr/sbin/ip link set dev enp1s0 promisc on
ExecStart=/usr/sbin/ethtool -K enp1s0 gro off lro off
TimeoutStartSec=0
RemainAfterExit=yes
[Install]
WantedBy=default.target
```

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXfTF_w0TuagyCwIbcPNbPqczxcPQqbmCyDgWQGgxbliyX2k_he2g7DcjzE4hIS81CUU92euNPcHMrsFF6NVSUbi4xKTAZSHif4MZsW7RG4nTx79OvYxcnhZqvDHCPyT7ySzz2TThqKhzDiRw1GQvb6Z6JGL?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfTF_w0TuagyCwIbcPNbPqczxcPQqbmCyDgWQGgxbliyX2k_he2g7DcjzE4hIS81CUU92euNPcHMrsFF6NVSUbi4xKTAZSHif4MZsW7RG4nTx79OvYxcnhZqvDHCPyT7ySzz2TThqKhzDiRw1GQvb6Z6JGL?key=REBS4JzpPJr9JzQsSLcUIg)

Este servicio configura la interfaz de red enp1s0 para funcionar en modo promiscuo y desactiva las **optimizaciones GRO y LRO** al iniciar el sistema.

Ahora guardamos y recargamos el daemon, luego habilitamos y arrancamos el servicio.

```html
**sudo systemctl daemon-reload
sudo systemctl enable snort3-nic.service
sudo systemctl start snort3-nic.service**
```

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXcFFZ-K4KvSM0FaD-cJrmbr4n2FrrCB5fOecI_KE1hlxIpjZFbXTU42hiciEBwSKkmBrdSMUtU116W3YaVaExOlSg_brTkHAHNFLp9KWK_yheC_hTdLiY3TIN2Vov2897xWG75FFDNblll_2nFaEI_bnDPA?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcFFZ-K4KvSM0FaD-cJrmbr4n2FrrCB5fOecI_KE1hlxIpjZFbXTU42hiciEBwSKkmBrdSMUtU116W3YaVaExOlSg_brTkHAHNFLp9KWK_yheC_hTdLiY3TIN2Vov2897xWG75FFDNblll_2nFaEI_bnDPA?key=REBS4JzpPJr9JzQsSLcUIg)

**Pasamos a analizar el archivo de configuración snort.lua de snort:**

En la primera parte se configura tanto la red interna que queremos proteger como la red externa, que en nuestro caso van a ser todas menos la red interna

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXfh-p46KJJqotVF_pdAdw9xGi4WiXxoost_wTsL-J_r_d_LwBbnuE9bFcuwAmYzqSPVdXr1jpBm3LAOLifITJ1KRYavtnOAmCbSSxczGub9zaQ50FkOp5UKCfRYjueucmUOOiIRuVmg2VOXFppzpKdwXs2u?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfh-p46KJJqotVF_pdAdw9xGi4WiXxoost_wTsL-J_r_d_LwBbnuE9bFcuwAmYzqSPVdXr1jpBm3LAOLifITJ1KRYavtnOAmCbSSxczGub9zaQ50FkOp5UKCfRYjueucmUOOiIRuVmg2VOXFppzpKdwXs2u?key=REBS4JzpPJr9JzQsSLcUIg)

Luego nos encontramos con los diferentes módulos de inspección que analizan tipos de tráfico y protocolos

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXeprVO2NL1569udfH0TwxbrLCx96GQJGMIl2rinr30CpGoe6mU0TeHXh1AsJcW8_hTE3A0ANQrm3NHrKy3Ld6uZ50vqTdFLP8-ZxPvGgpODtkXW1ek0QYrgns4eG73JdwMdwCDgh_52xoA3jiLR-qPS3O4?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeprVO2NL1569udfH0TwxbrLCx96GQJGMIl2rinr30CpGoe6mU0TeHXh1AsJcW8_hTE3A0ANQrm3NHrKy3Ld6uZ50vqTdFLP8-ZxPvGgpODtkXW1ek0QYrgns4eG73JdwMdwCDgh_52xoA3jiLR-qPS3O4?key=REBS4JzpPJr9JzQsSLcUIg)

Lo siguiente que aparece son las vinculaciones (bindings), esta configuración asocia ciertos puertos y protocolos con módulos específicos.

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXfFH5boj5NKS4rMqtqI5oExOxYky55qc3nOPxbUYclOOna9d1KlM2kLPnVw4_8YSOZ_bL_4jw5nEJk8rA4w_TcMHXYHonFvwu_2HP7ZTkQfteksEdDtMaJ7EuOkxZVwya4fUPBXtDaXqHlKbZBIhRfqrMk?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfFH5boj5NKS4rMqtqI5oExOxYky55qc3nOPxbUYclOOna9d1KlM2kLPnVw4_8YSOZ_bL_4jw5nEJk8rA4w_TcMHXYHonFvwu_2HP7ZTkQfteksEdDtMaJ7EuOkxZVwya4fUPBXtDaXqHlKbZBIhRfqrMk?key=REBS4JzpPJr9JzQsSLcUIg)

El siguiente parámetro a configurar es la sección que monitoriza el rendimiento

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXcL4yFB_JHyhhqhE3Zauah5_LITcuPOL3sVX6BToKFhWKzpJb2sTgS72JWA1sSvTtZBtHL38tC8CJZt5Pab55udiRGk3RH59MiJN3iIn5Y0oHqVeWOOvt2mF53EtwusbmlgZmAeXmcyar5SxpSN6a60Ni8f?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcL4yFB_JHyhhqhE3Zauah5_LITcuPOL3sVX6BToKFhWKzpJb2sTgS72JWA1sSvTtZBtHL38tC8CJZt5Pab55udiRGk3RH59MiJN3iIn5Y0oHqVeWOOvt2mF53EtwusbmlgZmAeXmcyar5SxpSN6a60Ni8f?key=REBS4JzpPJr9JzQsSLcUIg)

Luego nos encontramos con el apartado de detección, aquí configuraremos las reglas que Snort va a usar para detectar amenazas

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXda8OAxrHi5n-Up5HEGnudsxXRSoocJtYYDsOafWvbe9BfcJrNnjlwpfqXkFl3P2xLN5A2r7-tpwAsHbVPcxlqZwm_oBIeCPKV-ppPjzZR-70GaJ-T_yA8hv8e3ANsUXjcv7ECbOKslvL8Cg1hgmbUZn5F0?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXda8OAxrHi5n-Up5HEGnudsxXRSoocJtYYDsOafWvbe9BfcJrNnjlwpfqXkFl3P2xLN5A2r7-tpwAsHbVPcxlqZwm_oBIeCPKV-ppPjzZR-70GaJ-T_yA8hv8e3ANsUXjcv7ECbOKslvL8Cg1hgmbUZn5F0?key=REBS4JzpPJr9JzQsSLcUIg)

Lo siguiente son los filtros, que configuraremos más adelante en caso que los necesite.

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXdpWBjm8qR4aD0x_PmbP22-Ktz_T4ELEc3OXY9no1lyaPTv9NUFqM64KOw4GYg-WLCPmI2VqpZr_OS9f0xG3ELAY3gxJi4HKPvJRHrvLo2UhuUF5QPQX-ajsmvc6TMcEG3qIkuvnfskeF5YNnqXdRjp_Ro?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdpWBjm8qR4aD0x_PmbP22-Ktz_T4ELEc3OXY9no1lyaPTv9NUFqM64KOw4GYg-WLCPmI2VqpZr_OS9f0xG3ELAY3gxJi4HKPvJRHrvLo2UhuUF5QPQX-ajsmvc6TMcEG3qIkuvnfskeF5YNnqXdRjp_Ro?key=REBS4JzpPJr9JzQsSLcUIg)

Lo penúltimo que podremos configurar son las salidas (outputs), que son la configuración de logs y alertas, de igual manera configuraremos luego en caso necesario.

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXeLePC6tkU82ssTjLb3FKt5xrZ6SqXSjObJhxTuFih9qIhrvpslKayFSZThoEwCnhHTCssfJz4QMzCnLHTU3gAfrpbeV5V97te9oSMgakfMemG758yl3e2QhpGuY2gVoObcWLWpbo7d1--NFJWRi3nrEuU?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeLePC6tkU82ssTjLb3FKt5xrZ6SqXSjObJhxTuFih9qIhrvpslKayFSZThoEwCnhHTCssfJz4QMzCnLHTU3gAfrpbeV5V97te9oSMgakfMemG758yl3e2QhpGuY2gVoObcWLWpbo7d1--NFJWRi3nrEuU?key=REBS4JzpPJr9JzQsSLcUIg)

Y por último tenemos los tweks, que es una sección para incluir configuraciones adicionales si las necesitamos.

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXfNXQ837xmw8eb22Z3yluBOvL4XI11hES4pNwWpiDsl6khQJrbA2Bd3YAslQWW8AACVjSYJt852kPLdPg_qLG8xYnqCRUWynGrZJxAoB07Hjq9GlWPHXPl8NyViCh8PnblaftmTy1uQThzX17M1pZl5hUYP?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfNXQ837xmw8eb22Z3yluBOvL4XI11hES4pNwWpiDsl6khQJrbA2Bd3YAslQWW8AACVjSYJt852kPLdPg_qLG8xYnqCRUWynGrZJxAoB07Hjq9GlWPHXPl8NyViCh8PnblaftmTy1uQThzX17M1pZl5hUYP?key=REBS4JzpPJr9JzQsSLcUIg)

### **Instalación reglas de la comunidad**

Primero, creamos un directorio para almacenar todas las reglas:

**`sudo mkdir /usr/local/etc/rules`**

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXdTECZFu0Nqxv0gu-rTpIyggL3LCd-yeI2sVN3r1zJ8aPOkux4VXz_xnUgMZyDhf_MaYWX6AeJJVmlmXMC2EMAf_kumolkYHfEUr8whdfK8soK1mlqt_PVDWJrzVmAGbEJe8IDKbZRfVckTjiWM59I38HZZ?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdTECZFu0Nqxv0gu-rTpIyggL3LCd-yeI2sVN3r1zJ8aPOkux4VXz_xnUgMZyDhf_MaYWX6AeJJVmlmXMC2EMAf_kumolkYHfEUr8whdfK8soK1mlqt_PVDWJrzVmAGbEJe8IDKbZRfVckTjiWM59I38HZZ?key=REBS4JzpPJr9JzQsSLcUIg)

```html
**wget -qO- https://www.snort.org/downloads/community/snort3-community-rules.tar.gz | tar xz -C /usr/local/etc/rules/**
```

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXcYkyjHalLy3_wKYs3b_vu-A7Ky1OCAN_rfsmIR58IpdueB2yd7r6e-FpK2LqjewzyNrLTu_wu4wmRhtWDDYMJqWOwjAzbUjlQRO6X5SbUEBP-_4feirPtJmCIIXmzlKQifkjwKpDiefeq3xLlssQUXwZA?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcYkyjHalLy3_wKYs3b_vu-A7Ky1OCAN_rfsmIR58IpdueB2yd7r6e-FpK2LqjewzyNrLTu_wu4wmRhtWDDYMJqWOwjAzbUjlQRO6X5SbUEBP-_4feirPtJmCIIXmzlKQifkjwKpDiefeq3xLlssQUXwZA?key=REBS4JzpPJr9JzQsSLcUIg)

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXfmZuDi4dwCnWtBVYrOTEnuHERY4TsLoYnesUwzpqjLMH2V5jq8ZV0horRxs1p1a06ItJvY4_Y_NJsn9YcymDAcBZRLeY2A40u8Wa9SAkDR1PFErHVzab8omfTAM6ga_8mSDRISRq44COSOgC-vSYKTqpZt?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfmZuDi4dwCnWtBVYrOTEnuHERY4TsLoYnesUwzpqjLMH2V5jq8ZV0horRxs1p1a06ItJvY4_Y_NJsn9YcymDAcBZRLeY2A40u8Wa9SAkDR1PFErHVzab8omfTAM6ga_8mSDRISRq44COSOgC-vSYKTqpZt?key=REBS4JzpPJr9JzQsSLcUIg)

A continuación, editamos el archivo de configuración de Snort para definir nuestra red. Como ahora mismo estoy usando una máquina virtual variando entre las IPs de mi casa y del instituto, voy a configurarlo en la red default de kvm, es decir, la `192.168.122.0/24`

**`sudo nano /usr/local/etc/snort/snort.lua`**

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXeKsNRtLZ-ZYBoXCK3KiSsCNn4yQ6TuVD0kKzPcwttx-eiP1JS1kj9hj7kRpphvHxs__tslauv0smU9G9yEsRJnJ3jBlfXuUJZBTzH_ItYMVRaa_kn7NhSeh__9BR-3SItPxUhQdUizykw_NMERB5RQWvA?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeKsNRtLZ-ZYBoXCK3KiSsCNn4yQ6TuVD0kKzPcwttx-eiP1JS1kj9hj7kRpphvHxs__tslauv0smU9G9yEsRJnJ3jBlfXuUJZBTzH_ItYMVRaa_kn7NhSeh__9BR-3SItPxUhQdUizykw_NMERB5RQWvA?key=REBS4JzpPJr9JzQsSLcUIg)

Ahora vamos a configurar la ruta de nuestras reglas snort.

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXccPdjiV2CkmE5IzgxZW9piuLKSZs9KL16OGxb5qY8NK6wIK6VpMNFvJ7ZlBb3xNHwCNtlHhH7C1c88QyeHyHKrjXDAW5SxIrb40WhrECr2CrukSKXJBCb3grrZ2Odl49CwU1rtjB9wqYtvw2Qh3CqqDI4k?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXccPdjiV2CkmE5IzgxZW9piuLKSZs9KL16OGxb5qY8NK6wIK6VpMNFvJ7ZlBb3xNHwCNtlHhH7C1c88QyeHyHKrjXDAW5SxIrb40WhrECr2CrukSKXJBCb3grrZ2Odl49CwU1rtjB9wqYtvw2Qh3CqqDI4k?key=REBS4JzpPJr9JzQsSLcUIg)

Guardamos y salimos.

**Instalar Snort OpenAppID**

OpenAppID es un plugin que permite a Snort detectar varias aplicaciones, Facebook, Netflix, Twitter y Reddit, utilizadas en la red.

Para instalarlo haremos lo siguiente:

```html
**sudo wget https://www.snort.org/downloads/openappid/33380 -O OpenAppId-33380.tgz**
```

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXc1Jx8SRPLe0Mh_ayLHHMrQEArVuep58xP9BlxRQiSQtE5F2A_oaLczyF3GA0jDrUCuuIm9z50_1imGmHG0PlVWLVLd5ghnd0UC-PV8-uE7HFPIjR_tkYtlv3aDmdTqQeF_mXjDej5a-A_wW5gc2GRqvD4?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXc1Jx8SRPLe0Mh_ayLHHMrQEArVuep58xP9BlxRQiSQtE5F2A_oaLczyF3GA0jDrUCuuIm9z50_1imGmHG0PlVWLVLd5ghnd0UC-PV8-uE7HFPIjR_tkYtlv3aDmdTqQeF_mXjDej5a-A_wW5gc2GRqvD4?key=REBS4JzpPJr9JzQsSLcUIg)

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXe3xwKQGCtm4jc2wNkuoENcQsIjIZIVPZTNl1AWSmP_zP05o76-xHpFczZkOpyqWKaQtTu4J3vqK8YLdfSZCXu8Qt8cmEqp6B4y7ZJF7Q2uZPju5LjiTj9mT8BKCiR3WZX6dUf9m9shoazBwDHSvsahOo_0?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXe3xwKQGCtm4jc2wNkuoENcQsIjIZIVPZTNl1AWSmP_zP05o76-xHpFczZkOpyqWKaQtTu4J3vqK8YLdfSZCXu8Qt8cmEqp6B4y7ZJF7Q2uZPju5LjiTj9mT8BKCiR3WZX6dUf9m9shoazBwDHSvsahOo_0?key=REBS4JzpPJr9JzQsSLcUIg)

**`sudo tar -xzvf OpenAppId-33380.tgz`**

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXfDTt57yMr5gvoL5zdf6H3BVJ-qGgm80GaZ3FTf0pcFeUVrOd4QNWZ08ZKb59neDtjImxyIz9u9AO-zk_fqvio1qgMNxqbXmibN1EbzCqwhocfMkDEmsp12LS3VrhXk4W2e-0inFfXio_eKuwFuGiEXb-1C?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfDTt57yMr5gvoL5zdf6H3BVJ-qGgm80GaZ3FTf0pcFeUVrOd4QNWZ08ZKb59neDtjImxyIz9u9AO-zk_fqvio1qgMNxqbXmibN1EbzCqwhocfMkDEmsp12LS3VrhXk4W2e-0inFfXio_eKuwFuGiEXb-1C?key=REBS4JzpPJr9JzQsSLcUIg)

A continuación, copiamos el archivo binario de OpenAppID al directorio del sistema:

**`sudo cp -R odp /usr/local/lib/`**

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXdyscTg800zFZ4gLvaLQXcpIsDLQBrln-cn5N8P8z4SNxOQ-6zww0WmtcZFAgwF2xyphp6Og2Wm2fn29fxCoCsV6ML9_Brn9BwYEaTLj9kF5YaWrEbatBnHzWHAAyta6N_CISSJD5BkwKIkWyVqPBUGNOhg?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdyscTg800zFZ4gLvaLQXcpIsDLQBrln-cn5N8P8z4SNxOQ-6zww0WmtcZFAgwF2xyphp6Og2Wm2fn29fxCoCsV6ML9_Brn9BwYEaTLj9kF5YaWrEbatBnHzWHAAyta6N_CISSJD5BkwKIkWyVqPBUGNOhg?key=REBS4JzpPJr9JzQsSLcUIg)

A continuación, editamos el archivo de configuración de Snort y definimos la ubicación de OpenAppID:

**`sudo nano /usr/local/etc/snort/snort.lua`**

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXcFFr33NviGdaoL0nV39WFA79GpFxBvKF3VAlgWhykyuaTHZoQAi64KxRBezsgwY8I-mYA2NHnTbFF4um107hnL_oVL2dOy2Uw6wSxdxXpPXYuizLePFZSuPUdO1hzxgW7YpDVPFelwyz7MB_ocztQFOQM?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcFFr33NviGdaoL0nV39WFA79GpFxBvKF3VAlgWhykyuaTHZoQAi64KxRBezsgwY8I-mYA2NHnTbFF4um107hnL_oVL2dOy2Uw6wSxdxXpPXYuizLePFZSuPUdO1hzxgW7YpDVPFelwyz7MB_ocztQFOQM?key=REBS4JzpPJr9JzQsSLcUIg)

Guardamos el archivo, luego creamos un directorio de registro de Snort:

**`sudo mkdir /var/log/snort`**

Una vez tenemos configurado el plugin y las reglas de la comunidad, podemos usar el siguiente comando para comprobar que, efectivamente está leyendo las reglas que le hemos configurado:

**`sudo snort -c /usr/local/etc/snort/snort.lua`**

Vemos que tenemos configuradas 4225 reglas

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXd8eaYYAFTrxfKO1iNtKZ7EhM-gkRLCUCCwqg2_t_kWcnZfJPRBUcmDyc8eG_IY2VeRIibxxs-6V4Oq_EaXPJdPTaJ6faVfs6YaWdmt35mA6EPEOen5LYe6jIzS44SG6S2mc0ykVzs8-RHM0Ad4KmpW_Aqq?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXd8eaYYAFTrxfKO1iNtKZ7EhM-gkRLCUCCwqg2_t_kWcnZfJPRBUcmDyc8eG_IY2VeRIibxxs-6V4Oq_EaXPJdPTaJ6faVfs6YaWdmt35mA6EPEOen5LYe6jIzS44SG6S2mc0ykVzs8-RHM0Ad4KmpW_Aqq?key=REBS4JzpPJr9JzQsSLcUIg)

Y que hemos configurado todo de manera correcta gracias a este aviso

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXeJXnOxVxZIfQCJxXZfCzNTI9dFhne0Nt-GajD3CrRhwxPA7bcphz3aTyj96QyzLOMXpzzo54tVg67wYRT2HV9MtPxAvlTn6k7BY2SXsQQ5HD61T0EAfof4AVh06UzZX9KgzYn5AfjOhtqqXP4jYVgQYYk?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeJXnOxVxZIfQCJxXZfCzNTI9dFhne0Nt-GajD3CrRhwxPA7bcphz3aTyj96QyzLOMXpzzo54tVg67wYRT2HV9MtPxAvlTn6k7BY2SXsQQ5HD61T0EAfof4AVh06UzZX9KgzYn5AfjOhtqqXP4jYVgQYYk?key=REBS4JzpPJr9JzQsSLcUIg)

### **Reglas personalizadas de Snort y demostración de uso**

Una vez vista la configuración de Snort y su reglas de la comunidad, vamos a ver cómo podremos crear nuestras propias reglas. Las reglas de la comunidad están muy bien pero nos podemos ver en la tesitura de que sean demasiadas para lo que nosotros queremos, por ejemplo, si solo tenemos un servidor de bbdd que queremos proteger para que queremos cargar 2000 reglas de http, para ello vamos a pasar a ver cómo crear nuestras propias reglas y configurarlas de la manera que queramos.

Las reglas las vamos a crear en un archivo llamado snort.rules, este archivo se ubica en `/usr/local/etc/snort/rules`. Si no tenemos dicho repositorio lo creamos, la ubicación no importa mucho porque en la configuración de snort vamos a poner nosotros donde se ubica.

**`sudo nano /usr/local/etc/snort/rules/local.rules`**

Antes de empezar a configurar el archivo de reglas propias tenemos que saber cómo es la sintaxis de las reglas de Snort. La sintaxis es la siguiente:

Lo primero que vamos a poner es la acción que queramos realizar, hay varias opciones a elegir como alert, drop, reject, pass, dependiendo de lo que queramos usaremos unas u otras, por ejemplo si solo queremos que nos alerte de algo usamos alert, pero si queremos bloquear algo usaremos reject.

Luego va el protocolo, la red de origen, el puerto de origen hacia la red de destino, puerto de destino.

Una vez hecho esto podemos seguir especificando un mensaje, un sid que va a ser un identificador para esta alerta, podemos poner el que queramos y un rev. Rev identifica de forma única el número de revisión de una regla de Snort determinada. Esta opción debe usarse junto con la clave sid y debe incrementarse en uno cada vez que se realiza un cambio en una regla.

La sintaxis quedaría de esta forma :

**`[acción] [protocolo] [ip_orig] [puerto orig] -> [ip desti] [puerto dest] ([mensaje]; [sid]; [rev])`**

Y ya tendríamos la sintaxis de una regla, con este ejemplo se vería mejor

**`alert icmp any any -> $HOME_NET any (msg:”Prueba ping”; sid: 100001; rev: 1)`**

Esta regla avisará cuando haya un ping (protocolo icmp) desde cualquier red y cualquier puerto a nuestra red local (tenemos configurada la variable en el archivo de configuración snort.lua), a cualquier puerto de nuestro dispositivo y mostrará el mensaje prueba ping con identificador 100001 y revisión 1.

La sintaxis de las reglas son sencillas pero se puede hacer muy tediosa, para ello existe una herramienta que viene muy bien llamada snorpy ([http://www.cyb3rs3c.net/](http://www.cyb3rs3c.net/)) donde nos permite crear reglas propias de una manera mucho más sencilla.

Para entender y comprobar el funcionamiento de dichas reglas vamos a probar la que hemos puesto antes que es una regla muy sencilla. Cambiamos la configuración de snort.lua para que lea las reglas del archivo creado anteriormente

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXf20X1yfvpWavCFaMjjWFlvzi6c-OsClnSyW7brapqE5J1NvQNXp60xFEvfTL_2uu8mIyRrUIcAWYi9QytI-3wO-YPYATxPkq37RhqYzjW09mKy2ZHRnZAGr47y7syYTtU8jlU6gryn-VJP8N3RbX2FEPUq?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf20X1yfvpWavCFaMjjWFlvzi6c-OsClnSyW7brapqE5J1NvQNXp60xFEvfTL_2uu8mIyRrUIcAWYi9QytI-3wO-YPYATxPkq37RhqYzjW09mKy2ZHRnZAGr47y7syYTtU8jlU6gryn-VJP8N3RbX2FEPUq?key=REBS4JzpPJr9JzQsSLcUIg)

Una vez hecho esto ya podremos ejecutar snort, pero antes hay que entender bien qué opciones tenemos y cual nos convendría más usar.

Las opciones que vamos a usar de snort son las siguientes:

- **A** para usar el modo alerta, aquí podremos precisar qué modo de alerta queremos **console** para que nos lo muestre en la terminal, escribe las alertas en el archivo "alert" predeterminado en un mensaje de alerta en una sola línea, estilo syslog. **Full** escribe la alerta en el archivo "alert" con el encabezado completo decodificado, así como el mensaje de alerta. **None** desactiva las alertas. **Unsock** es un modo experimental que envía la información de alerta a través de un socket UNIX a otro proceso que se conecta a ese socket.
- **q** para ejecutarlo en modo silencioso, que no nos muestre todo el rato por pantalla todo.
- **l** esta opción establece el directorio de registro de salida en log-dir. Todas las alertas en texto plano y los registros de paquetes se guardan en este directorio. Si esta opción no se especifica, el directorio de registro predeterminado se establece en /var/log/snort.
- **i** para la interfaz
- **c** para especificar el archivo de configuración

Vamos a poner en práctica todas estas opciones junto a la regla creada anteriormente

**sudo snort -q -l /var/log/snort -i enp1s0 -c /usr/local/etc/snort/snort.lua -A Fast**

Ejecutamos el comando y ahora desde otra máquina de la red le haremos ping

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXfrpEWShdWOao1h13pJbHDia6s4ClDfTqtA0Mdfr2hzgmUHMtpssBUV1Six4BrlLqT0PW1e11ELYMRviRCNbhVaV_bS70pVADKp4hmJWQG_-PZvOjmTD9sUojdbRsMgJpk0CzCVPRRj6HIUgcojAuN5ooVZ?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfrpEWShdWOao1h13pJbHDia6s4ClDfTqtA0Mdfr2hzgmUHMtpssBUV1Six4BrlLqT0PW1e11ELYMRviRCNbhVaV_bS70pVADKp4hmJWQG_-PZvOjmTD9sUojdbRsMgJpk0CzCVPRRj6HIUgcojAuN5ooVZ?key=REBS4JzpPJr9JzQsSLcUIg)

Vemos que nos muestra las alertas con la fecha en la que se ha realizado y el mensaje que le hemos configurado.

Ahora vamos a probar otro tipo de reglas. Por ejemplo vamos a ver cómo se comportaría con ssh, para ello crearemos la siguiente regla:

**`alert tcp any any -> $HOME_NET 22 (msg:”Intento de conexion SSH”; sid:100002; rev:1)`**

Como observamos en la siguiente regla, el puerto de destino ha cambiado, ya no es any como en el ping, ahora especificamos el puerto de conexión ssh.

Vamos a agregar la regla a nuestro archivo local.rules y verificamos su funcionamiento

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXdlv7EiYdqmevNVl_P8LC8vwR35kOhgDGGy5BSrcJBOwFtmFRG2Lxv39S8gmxhtMhhht5RWNlyOLlkGyVU6uEd9mcjnkCaxezTMrmppqSEaNF4j2UDmhnDObRssMDmiVs469coeN-8ktedfhQGuCA8GvCLN?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdlv7EiYdqmevNVl_P8LC8vwR35kOhgDGGy5BSrcJBOwFtmFRG2Lxv39S8gmxhtMhhht5RWNlyOLlkGyVU6uEd9mcjnkCaxezTMrmppqSEaNF4j2UDmhnDObRssMDmiVs469coeN-8ktedfhQGuCA8GvCLN?key=REBS4JzpPJr9JzQsSLcUIg)

Ya agregadas, pasamos a su comprobación

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXcekian2tgxmTwHTxh8W_TLd4s234aYdM6yVfslbGYRnRSp2ogkSt_XS0_XJ56mxz2IT4pHPmwtpeWKr_JY8Ko4ESonU560nppjPyr_ZdTgF_oQyTpL8IAOc-QEXUPJe5GLMtO7k16Qjr2izhaVIvOuNLhP?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcekian2tgxmTwHTxh8W_TLd4s234aYdM6yVfslbGYRnRSp2ogkSt_XS0_XJ56mxz2IT4pHPmwtpeWKr_JY8Ko4ESonU560nppjPyr_ZdTgF_oQyTpL8IAOc-QEXUPJe5GLMtO7k16Qjr2izhaVIvOuNLhP?key=REBS4JzpPJr9JzQsSLcUIg)

Vemos que nos avisa quien se ha conectado por ssh.

Una vez hemos entendido el funcionamiento y la lógica de las reglas de Snort pasamos a lo más importante, cuántas reglas hacemos y de qué queremos que nos avise Snort.

Para este apartado me falta conocimiento en seguridad porque es la primera vez que veo algo relacionado con esto, por lo que no sé cuales son las vulnerabilidades más frecuentes o las más peligrosas.

Lo que voy a hacer es buscar todas las vulnerabilidades que tiene una máquina metasploitable 3 y crearé reglas para protegerla.

Para ello buscamos los puertos abiertos de mi máquina metasploitable 3 haciendo **sudo nmap -sV [ip_maquina]**, el -sV lo hacemos para que nos muestre los servicios con la versión de dicho servicio

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXcqjbJyjhM4d2egwGCvf4t6LgeITrGxFrTCJHOcHRM2xsBP-HJbJrbWL2MZuDWifUsYyB7BzOzU-lLrxInOQtgDFm5hB9Wel5SWiVgqUgROeNC8d8PvGUbU8LXDFUcpE27Ew38Ty7luXHFEDyIIgqHzujoh?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcqjbJyjhM4d2egwGCvf4t6LgeITrGxFrTCJHOcHRM2xsBP-HJbJrbWL2MZuDWifUsYyB7BzOzU-lLrxInOQtgDFm5hB9Wel5SWiVgqUgROeNC8d8PvGUbU8LXDFUcpE27Ew38Ty7luXHFEDyIIgqHzujoh?key=REBS4JzpPJr9JzQsSLcUIg)

Ya podemos observar todos los puertos abiertos de mi máquina metasploitable 3, para crear las reglas voy a usar la herramienta snopy2, que nos permite crear las reglas con una sencilla interfaz gráfica para hacer mucho menos tedioso el proceso.

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXcup4ZsbgB_50k2vh-TE76njewKcG4O5f-vGN3OJdDrdCq1-JW5LrczGzNBoBxCGJ1qWW2X2AjQB9DxQrOTMN2RApX-ea5F0KNhqc6hC5ktRfT2RPStdR5J0cU8OohuthmDXdHUa6cI-wK20kd5PxvOMdMS?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcup4ZsbgB_50k2vh-TE76njewKcG4O5f-vGN3OJdDrdCq1-JW5LrczGzNBoBxCGJ1qWW2X2AjQB9DxQrOTMN2RApX-ea5F0KNhqc6hC5ktRfT2RPStdR5J0cU8OohuthmDXdHUa6cI-wK20kd5PxvOMdMS?key=REBS4JzpPJr9JzQsSLcUIg)

Esta herramienta nos permite elegir la acción, el protocolo, ip y puerto de origen, ip y puerto de destino, sid, rev y el mensaje.

Hay varias opciones dependiendo de lo que queramos hacer, por ejemplo, si solo queremos que nos avise de si alguien está accediendo a algún puerto de los que están abiertos pondremos una regla alert, pero si queremos que solo las personas de la misma red se puedan conectar por cierto puerto haremos una regla reject.

Para que nos avise de cualquier persona que está accediendo a un puerto de los que están abiertos pondremo las siguientes reglas:

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXe7oCeTQ_TSwndbBlY5YV3mw6v37UDYaS8Nc8iQYqyUQzYVK49gmkrNAHBBB9-F2m66-T5TnEmIH9wWK5CelAd_0w0idrovFeoZvxu2oDgH27HaiBVrHVXHw1zAtM82v_nSDnCj0W3wbiAhdFvrSO1i0-w?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXe7oCeTQ_TSwndbBlY5YV3mw6v37UDYaS8Nc8iQYqyUQzYVK49gmkrNAHBBB9-F2m66-T5TnEmIH9wWK5CelAd_0w0idrovFeoZvxu2oDgH27HaiBVrHVXHw1zAtM82v_nSDnCj0W3wbiAhdFvrSO1i0-w?key=REBS4JzpPJr9JzQsSLcUIg)

Ya tenemos las reglas, estas reglas nos van a avisar si un dispositivo de cualquier red por cualquier puerto intenta acceder a la red que tenemos configurado en el **snort.lua**, en mi caso la `192.168.122.0/24` al puerto que le indiquemos según cada servicio. Dentro de esta red está la máquina metasploit. Ahora vamos a comprobar su funcionamiento

Para comprobar su uso voy a usar una máquina remota, es decir, tengo snort instalado en una máquina virtual que no es la metasploitable, voy a usar esa máquina para monitorizar la metasploitable.

Para que esto sea posible tenemos que asegurarnos que tenemos la interfaz configurada en modo promiscuo para que escuche todas las ips de la red

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXc6lFIiPNMOOJ5rWHgyecojEdl6peTyvZZ1VVtNUqH3CNj3_bWdodisZuw5ImjZUHKASy6nliWH4rBuOY3xfS-IA688pR8Mz-fGazIOVlFFNKX4YxcyKhaL5Fu4tHwMH7JE2B4MPA0P9IYiEPVdgX4hqGDz?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXc6lFIiPNMOOJ5rWHgyecojEdl6peTyvZZ1VVtNUqH3CNj3_bWdodisZuw5ImjZUHKASy6nliWH4rBuOY3xfS-IA688pR8Mz-fGazIOVlFFNKX4YxcyKhaL5Fu4tHwMH7JE2B4MPA0P9IYiEPVdgX4hqGDz?key=REBS4JzpPJr9JzQsSLcUIg)

En mi caso lo tengo correctamente configurado.

Ahora pasamos a la prueba, en una terminal estaré ejecutando snort y en la otra accediendo con metasploit a la máquina para acceder a una vulnerabilidad de esta.

Iniciamos metasploit en una terminal : **`msfconsole`**

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXdc_6J6mDCfLKaDwlYDBSApeekpagh_ATZrhcekQC1G7LPBIk2_nNM4-BTLp4OypxLqJauqfMSgDNPIjGjA3XDFMxUTzMpzaNWiB__A4t1C326LANXJTERMf-rcAx_OFloqD8GVFrrrLYkcHQWG12AXiNxX?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdc_6J6mDCfLKaDwlYDBSApeekpagh_ATZrhcekQC1G7LPBIk2_nNM4-BTLp4OypxLqJauqfMSgDNPIjGjA3XDFMxUTzMpzaNWiB__A4t1C326LANXJTERMf-rcAx_OFloqD8GVFrrrLYkcHQWG12AXiNxX?key=REBS4JzpPJr9JzQsSLcUIg)

Una vez abierta la consola de metasploit pasaremos a buscar el exploit de un servicio, por ejemplo el de ftp : **s`earch vsftpd 2.3.4`**

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXda_yRTiDJEgjAzBGCkcuLQZWKvWTn3iRUU_b2nM99lsHU2Rso6FVAPnTC7G1XVANX_-VhGN5yNe4Z5kvlY_YScREVo4eP2maJ_V_DBxdO7kMrJNdGqdCv20eGrTtvYWZQRVuiFKzoyf4PtB2jWWt9-sQOv?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXda_yRTiDJEgjAzBGCkcuLQZWKvWTn3iRUU_b2nM99lsHU2Rso6FVAPnTC7G1XVANX_-VhGN5yNe4Z5kvlY_YScREVo4eP2maJ_V_DBxdO7kMrJNdGqdCv20eGrTtvYWZQRVuiFKzoyf4PtB2jWWt9-sQOv?key=REBS4JzpPJr9JzQsSLcUIg)

Vemos que hay un exploit muy bueno para este servicio, porque nos permite entrar a la shell por una puerta trasera (backdoor, es un indicativo de que hay un error que nos va a permitir acceder a la terminal de dicha máquina sin que el dueño se de cuenta).

Procedemos a configurar el exploit, para ello haremos **use 0** para poder comenzar a configurar el exploit

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXebpSuS7mZGvZhAegIasuYYym74Kk8a0nPIh4FyWhG0nJL3vejcktxDpbhQo2VevcDoMTT89DLL2w3yaLyKwZ1LjtbxWCODg7YGEAkNIZsjJfaiQJatlGwh25K4wR_hMIUQRWEjqEMz7hxBRC9vnvcW9bzw?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXebpSuS7mZGvZhAegIasuYYym74Kk8a0nPIh4FyWhG0nJL3vejcktxDpbhQo2VevcDoMTT89DLL2w3yaLyKwZ1LjtbxWCODg7YGEAkNIZsjJfaiQJatlGwh25K4wR_hMIUQRWEjqEMz7hxBRC9vnvcW9bzw?key=REBS4JzpPJr9JzQsSLcUIg)

Ahora haremos un **show options** para ver que está configurado y que no.

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXduDY5LxXJRLJjhtqXzrZbdlHkk2qIeGyVUOZjDSEhGB8P0h7TI0_vr7wBUS95HbrRK5P9WVYTJhvyQi6TAIzVN5U2U2K7guuzYBkT9Hz90B3uW1HfwjYBen5vcPkZ8wAXYEPFuWDkTbHmjljHxmS98XcU?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXduDY5LxXJRLJjhtqXzrZbdlHkk2qIeGyVUOZjDSEhGB8P0h7TI0_vr7wBUS95HbrRK5P9WVYTJhvyQi6TAIzVN5U2U2K7guuzYBkT9Hz90B3uW1HfwjYBen5vcPkZ8wAXYEPFuWDkTbHmjljHxmS98XcU?key=REBS4JzpPJr9JzQsSLcUIg)

Vemos que el RHOST no está configurado por lo que el exploit no sabrá a qué máquina va a hacer el exploit, debemos configurar este parámetro con la IP del host que queremos atacar, para ello haremos **set rhost [ip]**

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXeAP1xivxa6tad0_2RSzs-BqFi8awaPml1E4aLIT_z_3_kIlr0El5h9z41P0uj5KnhedbCg11qO2-WBkLFXaRIebGi_B-iiKKIEKyOSveYnABQwI0tq9zKNOCX4K17LfQ-KQ_ELgZ976Q84OWlZ7KBOYx0G?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeAP1xivxa6tad0_2RSzs-BqFi8awaPml1E4aLIT_z_3_kIlr0El5h9z41P0uj5KnhedbCg11qO2-WBkLFXaRIebGi_B-iiKKIEKyOSveYnABQwI0tq9zKNOCX4K17LfQ-KQ_ELgZ976Q84OWlZ7KBOYx0G?key=REBS4JzpPJr9JzQsSLcUIg)

Una vez hecho ya tendremos configurado el host, pero nos falta un payload, el payload es el código que inyectamos en la máquina una vez ejecutado el exploit que nos permitirá abrir una shell inversa para poder tener acceso a la máquina.

Para ver los payloads que hay haremos **show payloads**

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXeaIs2JCsf5gUUMTap2prwQNkOBAoP84k4QiC2LhDrnO7GE14ClTImhdct5VIwZ1xLbI3x0WpW-GTpcvLfNldRsnbHweEvuwa4gpA2Er6V7ZN52dZZdx1elTGoeFotPhFCNVK4d6_w4Q4Tc-8whfRgqXdc?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeaIs2JCsf5gUUMTap2prwQNkOBAoP84k4QiC2LhDrnO7GE14ClTImhdct5VIwZ1xLbI3x0WpW-GTpcvLfNldRsnbHweEvuwa4gpA2Er6V7ZN52dZZdx1elTGoeFotPhFCNVK4d6_w4Q4Tc-8whfRgqXdc?key=REBS4JzpPJr9JzQsSLcUIg)

Vemos que solo hay 1 para este exploit, por lo que usaremos ese. Para configurarlo haremos **set payload 0**

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXceW_596Z36p_dTajrLyQtR-hUcZsZZHYv0IIJ4HzATfkjdOhtaAqo4Fg0C_yp7JHZStmVjWZ59-s826mt2DTBJkJuHxH638u72wjsomuU1W6Ew-QD6g303Da8wIwmol5S7AaZJPn6WKbpb0xSaQC-gXALK?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXceW_596Z36p_dTajrLyQtR-hUcZsZZHYv0IIJ4HzATfkjdOhtaAqo4Fg0C_yp7JHZStmVjWZ59-s826mt2DTBJkJuHxH638u72wjsomuU1W6Ew-QD6g303Da8wIwmol5S7AaZJPn6WKbpb0xSaQC-gXALK?key=REBS4JzpPJr9JzQsSLcUIg)

Ahora para ejecutar el exploit haremos run, pero antes de esto iniciamos snort para que nos monitoree el tráfico y nos avise de lo que vamos a hacer.

Lo haremos con este comando:

**`sudo snort -q -l /var/log/snort -i enp1s0 -A Fast -c /usr/local/etc/snort/snort.lua`**

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXcp6kzA92rzLGHQ7tptc8Vi8S_vq5Veiu0OBjOQqad8M7JJQbPnzpk7EbEKJpHln3g3nJDbQYhpSNlJ7g_wwad2ZQPNPw7TnNYnqiGYQ9pO6DBXgfpoQIg-iTQ3UAFjVuKle9vICX0jTe0N6IrE5mafL-s?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcp6kzA92rzLGHQ7tptc8Vi8S_vq5Veiu0OBjOQqad8M7JJQbPnzpk7EbEKJpHln3g3nJDbQYhpSNlJ7g_wwad2ZQPNPw7TnNYnqiGYQ9pO6DBXgfpoQIg-iTQ3UAFjVuKle9vICX0jTe0N6IrE5mafL-s?key=REBS4JzpPJr9JzQsSLcUIg)

Vemos que ya hemos accedido a la máquina usando el exploit, ahora comprobaremos los logs de Snort para ver si ha funcionado.

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXcZJN7PXw8mgn7B6ZaflVXQ00fAVqWiSrfiWa7QSQO1-fqYwWcsG3luqZxa3NctZdYt03yNyH1-imVTBfnDg2xT03SPm6h7nZAOO7fLN8XHxJqXDHpsFec-yIycLXDd_3ss2uyxzlFf1iICpzjIk0_c2r3F?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcZJN7PXw8mgn7B6ZaflVXQ00fAVqWiSrfiWa7QSQO1-fqYwWcsG3luqZxa3NctZdYt03yNyH1-imVTBfnDg2xT03SPm6h7nZAOO7fLN8XHxJqXDHpsFec-yIycLXDd_3ss2uyxzlFf1iICpzjIk0_c2r3F?key=REBS4JzpPJr9JzQsSLcUIg)

Vemos que los **logs** funcionan perfectamente.

Una vez explicado esto, haríamos lo mismo con todos los servicios que queramos proteger.

Para comprobar que lo podemos bloquear, haremos un reject sabiendo ya la dirección de donde viene.

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXdY8hfLpkleRKsqJavwmjgEGedBSzqVxH2-acx0L0DWDwONwvKBg49unlzMqYw5Vd1WGAawWTDOmctmanyMXe9IuqEG2rXAay4Fd79xliFd_t3l8RwAXaz88dgrZzvtSzq4KtBtqevMCg3Qykxz7EGyhHM?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdY8hfLpkleRKsqJavwmjgEGedBSzqVxH2-acx0L0DWDwONwvKBg49unlzMqYw5Vd1WGAawWTDOmctmanyMXe9IuqEG2rXAay4Fd79xliFd_t3l8RwAXaz88dgrZzvtSzq4KtBtqevMCg3Qykxz7EGyhHM?key=REBS4JzpPJr9JzQsSLcUIg)

Esto nos protegerá del exploit de dicha máquina, si queremos protegernos de todos los dispositivos menos los de nuestra red haríamos **$EXTERNAL_NET**.

Si quisiéramos bloquearlo a todo el mundo pondríamos **any** pero luego tendríamos que poner una regla de pass para que permita acceso a una máquina específica, porque sino no tendría sentido.

Vamos a probar que nos hemos protegido del exploit. Seguimos los mismos pasos para hacer el exploit que expliqué antes.

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXf9uuNTFZ3RsPR22ucPpvh-s6TPwlqVSM5lBc-TLuLxxGqJtJ2b9ryoDg8L1X114oOcXboBvL6QK4Sn7Krt0_FHqkOGjqKd54pWr2wIb616YSAFI0mBgVP6SNk1M1-Iqj2Ng0Y4l5YmD6yHxzh-8oaS4QMh?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf9uuNTFZ3RsPR22ucPpvh-s6TPwlqVSM5lBc-TLuLxxGqJtJ2b9ryoDg8L1X114oOcXboBvL6QK4Sn7Krt0_FHqkOGjqKd54pWr2wIb616YSAFI0mBgVP6SNk1M1-Iqj2Ng0Y4l5YmD6yHxzh-8oaS4QMh?key=REBS4JzpPJr9JzQsSLcUIg)

Como podemos observar, ya no nos deja entrar a la máquina gracias a la regla creada en Snort, para protegernos de todo haríamos lo mismo con todos los servicios que queramos.

### **Configuracióm del servidor de correo**

Para la configuración del servidor de correo con Snort usaré Postfix y lo configuraré para que me avise de las alertas que me detecte Snort, vamos a ello.

Primero de todo me voy a crear un correo solo para las alertas, se va a llamar [alertas.snort.raulhr@gmail.com](mailto:alertas.snort.raulhr@gmail.com), para ello nos vamos a la página de [www.gmail.com](http://www.gmail.com/) y lo creamos.

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXewA87ZFBSeACJKtOBGCw-OU9UXWLhBcXVc-eCKoFenI4Gs2sHtsfQXRkt_YLwRcrI5HJhQCzrzwa7VVUKytfxxtVHPTYOzA-rBwIheGrsi6UCIaUN4CFUGo36dv8lIlQHbNciLHQ9BbOZZ7aE9vTq0MFE?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXewA87ZFBSeACJKtOBGCw-OU9UXWLhBcXVc-eCKoFenI4Gs2sHtsfQXRkt_YLwRcrI5HJhQCzrzwa7VVUKytfxxtVHPTYOzA-rBwIheGrsi6UCIaUN4CFUGo36dv8lIlQHbNciLHQ9BbOZZ7aE9vTq0MFE?key=REBS4JzpPJr9JzQsSLcUIg)

Una vez creado nos vamos a los ajustes, para ello le daremos a gestionar tu cuenta de google en el siguiente apartado que se encuentra clicando sobre tu logo en la esquina superior derecha.

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXfNcU8Gpw0OymCoV9wU56pFb-6OxGXH7L4zxxyxQ7DbQPtpOCjjihjTvmULkQw1U913nMAaTxoY4vYkIfKqjWrnqFdkXQbitVL4s2sZ9zzVDbHFV9WrxTBUVex3_mq0HkXRchyzeBG8vTZu9oJlLC55Hipf?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfNcU8Gpw0OymCoV9wU56pFb-6OxGXH7L4zxxyxQ7DbQPtpOCjjihjTvmULkQw1U913nMAaTxoY4vYkIfKqjWrnqFdkXQbitVL4s2sZ9zzVDbHFV9WrxTBUVex3_mq0HkXRchyzeBG8vTZu9oJlLC55Hipf?key=REBS4JzpPJr9JzQsSLcUIg)

Una vez le demos a gestionar tu cuenta de Google nos llevará a otra ventana, ahí tendremos que darle en el apartado de **seguridad**, configuramos la **verificación en dos pasos** porque sino no nos sale lo que queremos

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXdgderebuUmcOrWlCJVQ5FgLEdJYGY65_LDdjqF2lhyA8r4GwUDVot36xxuPPgc7cghCleNnBcxGHdfaliaMf7-lr1fs4BQzeJW_aJ4b9q9LEMXX0G73xp065_-o8IrWoCalFs1Wu1kozQdX3i66cj2b38?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdgderebuUmcOrWlCJVQ5FgLEdJYGY65_LDdjqF2lhyA8r4GwUDVot36xxuPPgc7cghCleNnBcxGHdfaliaMf7-lr1fs4BQzeJW_aJ4b9q9LEMXX0G73xp065_-o8IrWoCalFs1Wu1kozQdX3i66cj2b38?key=REBS4JzpPJr9JzQsSLcUIg)

Una vez activada vamos al buscador superior e introducimos **contraseñas de aplicaciones**

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXffFFNYNNb6r0j0cxeAMBatOty8pjGP12XuI4ySucr0xCc3ZcelM2n-NjM6JS8rQzPWsHJGjSbtpYCsfe-qls3PYDJMehO5xDTacHxQkG1zs3F3txiLGddrc7EGZ2Py3AUYubsc3HmuhQsbtSaAplNc4pXJ?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXffFFNYNNb6r0j0cxeAMBatOty8pjGP12XuI4ySucr0xCc3ZcelM2n-NjM6JS8rQzPWsHJGjSbtpYCsfe-qls3PYDJMehO5xDTacHxQkG1zs3F3txiLGddrc7EGZ2Py3AUYubsc3HmuhQsbtSaAplNc4pXJ?key=REBS4JzpPJr9JzQsSLcUIg)

Introducimos **Postfix**

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXcwDua4rGvV70BxO6bBRUgn35rFDE6W2OTtRpB5iTSJqtFGzn1vN35-GlFrAqU9TNZVoG9lKtEFi3VuJ01GGbOQD_BwQoCw0-Elu632ePfD6mj2gx1iz6exzIvxNViaOx37c1ma0JdHYa3xyqbpFDsuw5Kz?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcwDua4rGvV70BxO6bBRUgn35rFDE6W2OTtRpB5iTSJqtFGzn1vN35-GlFrAqU9TNZVoG9lKtEFi3VuJ01GGbOQD_BwQoCw0-Elu632ePfD6mj2gx1iz6exzIvxNViaOx37c1ma0JdHYa3xyqbpFDsuw5Kz?key=REBS4JzpPJr9JzQsSLcUIg)

Una vez le demos a crear nos mostrará en pantalla nuestra contraseña, esta la guardaremos borrando los espacios que tiene Ahora pasamos a instalarnos postfix y configurarlo.

Lo primero que haremos para instalar postfix será **sudo apt install postfix -y**

A la hora de instalamos clicamos en la siguiente configuración

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXfB5RMOlZjFixeeqy224lpNIc1a2Xj4GWUG2ojuO-aM0NE8QGm4rtt1neGq9BYTj-JokwXBt4A2JnmVpkIVOK7fWcHmpc_rgjkupR1RL2StJbNM4YQccEMKx4dcGLn09aX2VI9fBkb_Zzj6CrU-NNMApB27?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfB5RMOlZjFixeeqy224lpNIc1a2Xj4GWUG2ojuO-aM0NE8QGm4rtt1neGq9BYTj-JokwXBt4A2JnmVpkIVOK7fWcHmpc_rgjkupR1RL2StJbNM4YQccEMKx4dcGLn09aX2VI9fBkb_Zzj6CrU-NNMApB27?key=REBS4JzpPJr9JzQsSLcUIg)

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXef-LmD--mRxZcvFbSmxGzXPtTSHW3kFg1GWaLAgHIRWS8D9INt685yjCLZUsfIegi972GcbwW6l1uSn-J5062NUOMs3QzMv0FrVEwBTwzoH0TPkHBn2FKHIOK8JR6ZbSnpjoLaK0FU8pLk3Qg_r8JJB6Xe?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXef-LmD--mRxZcvFbSmxGzXPtTSHW3kFg1GWaLAgHIRWS8D9INt685yjCLZUsfIegi972GcbwW6l1uSn-J5062NUOMs3QzMv0FrVEwBTwzoH0TPkHBn2FKHIOK8JR6ZbSnpjoLaK0FU8pLk3Qg_r8JJB6Xe?key=REBS4JzpPJr9JzQsSLcUIg)

Una vez instalado podemos proceder a configurarlo, para ello modificaremos el archivo **/etc/postfix/main.cf**

Configuraremos dicho archivo de la siguiente manera

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXdTOTUrglnXrGk4YJL6wFQg_KVHOW13l4lagfWFz4SlhCiAVJXkxVKfYd-71lIkVXanxU9iuKy09_RdCu017OczojZSuoRS6hhrHt5FmW6W2fJwjPxfwQgQSdX45GmEpn8oioamafHh-t_e0dlwIa0vvX4?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdTOTUrglnXrGk4YJL6wFQg_KVHOW13l4lagfWFz4SlhCiAVJXkxVKfYd-71lIkVXanxU9iuKy09_RdCu017OczojZSuoRS6hhrHt5FmW6W2fJwjPxfwQgQSdX45GmEpn8oioamafHh-t_e0dlwIa0vvX4?key=REBS4JzpPJr9JzQsSLcUIg)

Dicha información corresponde a lo siguiente:

<aside>
💡

**smtpd_banner:** Configura el mensaje de bienvenida del servidor.
**biff:** Desactiva notificaciones de correos nuevos.
**append_dot_mydomain:** Controla si se agrega el dominio automáticamente al nombre de host.
**smtp_use_tls, smtp_tls_CApath, smtp_tls_CAfile:** Activan el cifrado TLS y definen las rutas para certificados de confianza.
**smtpd_tls_cert_file, smtpd_tls_key_file:** Definen los certificados y claves para conexiones seguras entrantes.
**smtp_sasl_auth_enable:** Habilita la autenticación SMTP.
**smtp_sasl_password_maps:** Ubicación de credenciales para el servidor de retransmisión.
**smtp_sasl_security_options:** Configura opciones de seguridad (desactiva “no anónimo”).
**relayhost:** Define el servidor que usará Postfix para enviar correos (Gmail).
**smtpd_relay_restrictions:** Define quién puede enviar correos usando el servidor.
**myhostname:** Nombre de host del servidor.
**mydestination:** Dominios locales aceptados para entrega de correos.
**mynetworks:** Rangos de IP permitidos para usar el servidor sin autenticación.
**inet_interfaces, inet_protocols:** Definen interfaces y protocolos de red para escuchar.

</aside>

Ahora crearemos el archivo **sasl_passwd** para almacenar la información de nuestro correo junto a la contraseña que nos ha otorgado anteriormente (Donde he puesto $passwd tenemos que poner la contraseña que nos da gmail, porque este archivo no lee las variables de la bash)

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXcDlq0bpQH7oMuWtLjdiYe1Mdr-2k2T5wShfIpr75TDW6QvvD4GF1CqGNl2M4dGL5xeqQnboaHRbR55bU9nPQ8epeC5XdO0oMu4kwohzOzIYxnBbKvpW6x7Vfk4JpLnaUR-27xFAt2pFOU35bL2Jbk3zcPo?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcDlq0bpQH7oMuWtLjdiYe1Mdr-2k2T5wShfIpr75TDW6QvvD4GF1CqGNl2M4dGL5xeqQnboaHRbR55bU9nPQ8epeC5XdO0oMu4kwohzOzIYxnBbKvpW6x7Vfk4JpLnaUR-27xFAt2pFOU35bL2Jbk3zcPo?key=REBS4JzpPJr9JzQsSLcUIg)

Ahora hacemos **sudo postmap /etc/postfix/sasl_passwd** para convertir el archivo `/etc/postfix/sasl_passwd` en un formato de base de datos que Postfix pueda leer.

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXcdRGvV4hKutvTnc2HyPb2DkzowPRgh6PRunG04noCyQbW-JKeYOMLFc3t4SAp11fIo2HRTpGizmrxH_ogJ3fSf3fXVmZDCEi6g_FEErgMf7Y4LbWwwPKA0xVx40H56DLJ4Z7mDT0S6DoZKK8AFLz7FpaEC?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcdRGvV4hKutvTnc2HyPb2DkzowPRgh6PRunG04noCyQbW-JKeYOMLFc3t4SAp11fIo2HRTpGizmrxH_ogJ3fSf3fXVmZDCEi6g_FEErgMf7Y4LbWwwPKA0xVx40H56DLJ4Z7mDT0S6DoZKK8AFLz7FpaEC?key=REBS4JzpPJr9JzQsSLcUIg)

Y le cambiamos los permisos para que no estén muy abiertos

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXesgtELrSOsUPWIyN-G6xpEGz0ICW7DkUGGLhgXHiCRpeSVqRyGjS_q-XG61KTUjzwN5AmJNblBUmXsocsv8PoKkfdkZckU7Sol40uKnwWd67mHsZqgbKBzEZkB2w16UTD0N-Dmt_e5S0SCkGL1l0gCSJs?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXesgtELrSOsUPWIyN-G6xpEGz0ICW7DkUGGLhgXHiCRpeSVqRyGjS_q-XG61KTUjzwN5AmJNblBUmXsocsv8PoKkfdkZckU7Sol40uKnwWd67mHsZqgbKBzEZkB2w16UTD0N-Dmt_e5S0SCkGL1l0gCSJs?key=REBS4JzpPJr9JzQsSLcUIg)

Ahora vamos a recargar el servicio postfix y vamos a crear un script y un servicio para poder tener siempre que queramos activos los avisos de Snort.

Recargamos el servicio **`sudo /etc/init.d/postfix reload`**

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXdwCZaCzFJkb4m-wEsdlvG1v03o3U0718Po7K4uOWUM7BOhREhdVF5MJchcx9vPmJsgPo8WxNsno9N5Wzjmt3IaPQ2V2h9kW4np1-C11az_T17dNHdoBv2HShARbkKgM5cpdNDknNzr4ZQWgqDGL1F5S75P?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdwCZaCzFJkb4m-wEsdlvG1v03o3U0718Po7K4uOWUM7BOhREhdVF5MJchcx9vPmJsgPo8WxNsno9N5Wzjmt3IaPQ2V2h9kW4np1-C11az_T17dNHdoBv2HShARbkKgM5cpdNDknNzr4ZQWgqDGL1F5S75P?key=REBS4JzpPJr9JzQsSLcUIg)

Antes de crear el script para automatizar vamos a probar que nos funciona:

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXeDsJkEm6-ZxcCntw8K_0FOYowvPYUiDKkZuUA-IWzpJ1Wkmqc9ANYyBzuB82QpEWPDoRCINltX5LSFON5ne6rbrTE-cw2dhaAerNU8siY5GJSBhxakmZTAEV9WGYrkVH6553nZtR44rFQsDFzNuKccJX8?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeDsJkEm6-ZxcCntw8K_0FOYowvPYUiDKkZuUA-IWzpJ1Wkmqc9ANYyBzuB82QpEWPDoRCINltX5LSFON5ne6rbrTE-cw2dhaAerNU8siY5GJSBhxakmZTAEV9WGYrkVH6553nZtR44rFQsDFzNuKccJX8?key=REBS4JzpPJr9JzQsSLcUIg)

Vemos que nos ha llegado

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXdT5dquegWwyyp0P9WX6P8R_iYlZ2V12SeqRO11H5hjkf0Ycar9Wxl2e-PXdJv5gyTmRfEYHj2lLTDFy-XHOG4-jjPBJmllGIv_d5PLkLF93K540bgtanXIYH-gGDsOqoADXxQ-8_Dbg9rtWBridS9vsgUo?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdT5dquegWwyyp0P9WX6P8R_iYlZ2V12SeqRO11H5hjkf0Ycar9Wxl2e-PXdJv5gyTmRfEYHj2lLTDFy-XHOG4-jjPBJmllGIv_d5PLkLF93K540bgtanXIYH-gGDsOqoADXxQ-8_Dbg9rtWBridS9vsgUo?key=REBS4JzpPJr9JzQsSLcUIg)

Ahora vamos a empezar a crear y configurar el script para automatizar todo esto.

Lo primero que haremos será cambiar la configuración de Snort para que guarde los logs en un archivo de texto, para ello modificamos las siguiente líneas

**`sudo nano /usr/local/etc/snort/snort.lua`**

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXf4uCxSKptsVKdT9sSY_p0gK0IkOInol4OdoTBcKrJnZN_MKpZaKi00u4_l3bp0SHuCtx3XDd8Lp9MPjIP7vZa21E9szTBpB4ZBoRzqJPFefUBi63c55XWCEW5ifY4GWNNwhdL7NlBLuMkThT1YL_VYnWUa?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf4uCxSKptsVKdT9sSY_p0gK0IkOInol4OdoTBcKrJnZN_MKpZaKi00u4_l3bp0SHuCtx3XDd8Lp9MPjIP7vZa21E9szTBpB4ZBoRzqJPFefUBi63c55XWCEW5ifY4GWNNwhdL7NlBLuMkThT1YL_VYnWUa?key=REBS4JzpPJr9JzQsSLcUIg)

Activamos los 3 modos de alerta para que cuando usemos cualquiera de ellos nos cree el .txt

Una vez configurado snort, vamos a crear el **script**, este paso es bastante complejo por lo que hay que seguir los pasos al pie de la letra.

Lo primero que he hecho ha sido crear un script, pero me encontré con el primer problema.

Snort permite mostrar la información de varias maneras usando la opción -A, las más usadas son csv, fast y full (explicadas en el apartado de reglas propias), teniendo esto en cuenta creé un script donde manejaba las 3 opciones, pero probando con muchas combinaciones y de muchas maneras me seguían dando errores. Por lo que he decidido particionarlo y crear un script para cada opción con su respectivo servicio y así puedo manejar por separado las opciones que quiera.

Para comenzar debemos entender la lógica que queremos llevar y lo que queremos hacer en el script. Cuando Snort se ejecuta guarda el registro de las alertas en un archivo .txt dentro de la carpeta logs, sabiendo eso lo que haremos será crear otro archivo .txt, lo llamaremos comparador para entenderlo mejor, compararemos el tamaño del archivo que crea snort con el archivo comparador, si es más grande el archivo de snort se enviará el contenido de dicho archivo a mi correo con un aviso y se guardará en el archivo comparador para que la próxima vez que itinere el bucle no me envie nada ya que ambos archivos van a tener el mismo texto. Sabiendo esto vamos a comenzar con la configuración.

Lo primero que haremos será crear los archivos comprobadores

```html
**sudo touch /var/log/snort/ultima_linea_csv.txt
sudo touch /var/log/snort/ultima_linea_fast.txt
sudo touch /var/log/snort/ultima_linea_full.txt**
```

Una vez hecho esto ya tenemos los archivos contenedores, ahora vamos a cambiar el dueño de estos archivos a debian para después poder usarlos bién en el script.

**`sudo chown debian: /var/log/snort/u*`**

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXfvKEYOXFj_pVPo0yhFJE8m0T0ftSkBHN4ZfPT7icMoiLGadJJkI-tnvzfF7UtUmV5gpRV3Ze2_iIPHrokuvCH8WLN_n9AvWldtDSYcqJG_pUo8QDdnO27haDBdQ603GfMyCFGhvwbrjJ5hY1p9MlQpbTR8?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfvKEYOXFj_pVPo0yhFJE8m0T0ftSkBHN4ZfPT7icMoiLGadJJkI-tnvzfF7UtUmV5gpRV3Ze2_iIPHrokuvCH8WLN_n9AvWldtDSYcqJG_pUo8QDdnO27haDBdQ603GfMyCFGhvwbrjJ5hY1p9MlQpbTR8?key=REBS4JzpPJr9JzQsSLcUIg)

Una vez hecho esto procedemos a crear los 3 scripts, van a ser los 3 iguales cambiando solo el nombre de las variables por lo que voy a mostrar y explicar 1 solo.

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXfYUZC1cRY1O7ct6RwH3sEVq0-KmJ6k47yW_02RNcL3zoXXJLBLKNPL_hEt1GUXzpcc3t7a9OldOqxKit8jdwTbFhhUx_dv5vA200IFrvJaL24_rCAtZLxGnmfSmPFzo7auWrXGkwijpg05H2qqRMy2GDHS?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfYUZC1cRY1O7ct6RwH3sEVq0-KmJ6k47yW_02RNcL3zoXXJLBLKNPL_hEt1GUXzpcc3t7a9OldOqxKit8jdwTbFhhUx_dv5vA200IFrvJaL24_rCAtZLxGnmfSmPFzo7auWrXGkwijpg05H2qqRMy2GDHS?key=REBS4JzpPJr9JzQsSLcUIg)

Este script es el del modo csv, lo primero que hacemos es indicar los archivos que vamos a usar en las variables.

Luego empezamos un bucle para que esté constantemente mirando si hay cambios en la configuración y aquí viene una gran pregunta ¿Para qué quieres hacer un bucle que esté todo el rato funcionando en vez de solo cuando esté ejecutándose snort?

La respuesta es sencilla, porque no he encontrado otra forma mejor de hacerlo. Si configuro el script para que me inicie cuando ejecute x comando de snort, si por ejemplo, cambio la interfaz donde escucha snort ya no me funciona el script, para evitar todos esos errores lo dejo todo el rato funcionando y ya está.

Una vez comenzamos a itinerar el bucle pasamos el contenido de linea_csv (el tamaño que tiene el archivo de snort) al comparador para que la próxima vez que itinere no nos envíe nada, luego hago un if para comparar el archivo de snort con el comparador que creé antes, si el contenido de snort es mayor significa que hay contenido nuevo del cual no he sido notificado, para ello hacemos un tail -n del número que hay de diferencia y del fichero de snort para que nos muestre las líneas de texto de las cuales no hemos sido avisados, esto se guarda en una variable y se nos envía por correo.

Una vez tenemos el script configurado viene la siguiente duda, como puedo ejecutar el script todo el rato para que no me tenga que preocupar de él. Para ello vamos a crear un servicio que nos ejecute cada script, en este caso crearemos 3 servicios uno para cada modo, de la misma forma seguiré explicando solo el de csv porque los otros son exactamente iguales cambiando las letras csv por fast o full.

Para crear un servicio lo configuramos de la siguiente forma

**`sudo nano /etc/systemd/system/snort-alert-email-csv.service`**

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXdRHajkq8CGMDt-LEBcs-bjmOfP-IHCI_MuyD4pnlddKybzz-iqGxe6XTXgqXifaWvPvHf24gXE6DRPHJAH5uUAqkwSlMfrkRnDzD86XV9heRKXfb2xNWCOXNZFr5Jqm9oe2h37fCfz0izXPbb2fj4RMVPz?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdRHajkq8CGMDt-LEBcs-bjmOfP-IHCI_MuyD4pnlddKybzz-iqGxe6XTXgqXifaWvPvHf24gXE6DRPHJAH5uUAqkwSlMfrkRnDzD86XV9heRKXfb2xNWCOXNZFr5Jqm9oe2h37fCfz0izXPbb2fj4RMVPz?key=REBS4JzpPJr9JzQsSLcUIg)

Este servicio va a ejecutar el .sh todo el rato. Vemos que se ejecuta correctamente

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXcL2lKQ6C4iTCW_kODABht4weiq6I30HZ4JQk-VhqJIjAkSMIW4-7RCUlV28HcSh2si58svMUQTOx9_fikn8dao8SNUXTqwJSPx69rzQitd3CLU-yO3B64UMDcZDGBglD_tXg-slyW0DhXbX1BpIYhZ85w?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcL2lKQ6C4iTCW_kODABht4weiq6I30HZ4JQk-VhqJIjAkSMIW4-7RCUlV28HcSh2si58svMUQTOx9_fikn8dao8SNUXTqwJSPx69rzQitd3CLU-yO3B64UMDcZDGBglD_tXg-slyW0DhXbX1BpIYhZ85w?key=REBS4JzpPJr9JzQsSLcUIg)

Una vez tenemos el script y el servicio vamos a comprobar su funcionamiento

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXdTM3DIn6Vb0GjWoK2qolfbFk7a12DySlB1LDM0QMEg6tdpX5NkKddgIY-sy4QX78po-re7pjC2hu-JQlPtwisjlutOGLHMfxadrzEdRm8-_LDU3UedDmNn8dBUHjHiI9lNwwDuMCrdF1U5WiZ4h36Os1w?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdTM3DIn6Vb0GjWoK2qolfbFk7a12DySlB1LDM0QMEg6tdpX5NkKddgIY-sy4QX78po-re7pjC2hu-JQlPtwisjlutOGLHMfxadrzEdRm8-_LDU3UedDmNn8dBUHjHiI9lNwwDuMCrdF1U5WiZ4h36Os1w?key=REBS4JzpPJr9JzQsSLcUIg)

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXc-VhnxyjXfptyal7Lpkl9fdHFM4JgIgIa3Z80tbZDTm7re68LFaFXG8011qlos30vRQ26JuGM7Pgg1eazjLrW8Xg6QjTAtkLYmqdB5TMCGir1XNv3ryx0MoS5WXva78A8vf231ZoTaGm8MMA_uO_Xq8G4?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXc-VhnxyjXfptyal7Lpkl9fdHFM4JgIgIa3Z80tbZDTm7re68LFaFXG8011qlos30vRQ26JuGM7Pgg1eazjLrW8Xg6QjTAtkLYmqdB5TMCGir1XNv3ryx0MoS5WXva78A8vf231ZoTaGm8MMA_uO_Xq8G4?key=REBS4JzpPJr9JzQsSLcUIg)

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXfxLFN-tLEfg2UMCKgpHsI_8zLHhfzyWQwiFnhi5FGvFwpa2EXJ8TzyThHwq1Qu0e4f7oCI_HF15yMDgd-H2N1W1XoaqjfpM3a3yE1Iwxbq-7cbqZNgtu0MNbMny8wdmZv5SvOsf3kKa_jTYC62ir9olag9?key=REBS4JzpPJr9JzQsSLcUIg](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfxLFN-tLEfg2UMCKgpHsI_8zLHhfzyWQwiFnhi5FGvFwpa2EXJ8TzyThHwq1Qu0e4f7oCI_HF15yMDgd-H2N1W1XoaqjfpM3a3yE1Iwxbq-7cbqZNgtu0MNbMny8wdmZv5SvOsf3kKa_jTYC62ir9olag9?key=REBS4JzpPJr9JzQsSLcUIg)

Aquí podemos observar su correcto funcionamiento.

# Andrés Morales - Alumno 3

## Tripwire

### Introducción

El control de la integridad de ficheros y directorios no se realiza manualmente, como hacían los antiguos egipcios, sino mediante una herramienta que nos permite tener toda la información del estado inicial de estos elementos. Esto facilita la comparación con su estado actual en el futuro.

Para este propósito, utilizamos **Tripwire**, una herramienta de seguridad que, en esencia, es un comparador de integridad de ficheros y directorios UNIX. Funciona comparando un conjunto de información sobre estos elementos, almacenada en una base de datos, y envía alertas al administrador en caso de que ocurra algún cambio.

Esta herramienta de integridad de ficheros, desarrollada por la Universidad de Purdue, es la más conocida desde su lanzamiento en 1992.

El mecanismo de seguridad es bastante simple y realiza lo siguiente:

1. Crea un resumen de cada fichero y/o copia importante inmediatamente después de instalar el sistema.
2. Guarda esta información en un medio seguro (protegido contra escritura).
3. Alerta sobre cualquier modificación cada vez que se realiza una comprobación.

Para crear estos resúmenes, se utilizan funciones hash, lo que hace imposible que se generen dos archivos con el mismo resumen.

Esto se implementa mediante **MD2, MD3, MD5, Snefru, CRC-16 y CRC-32.**

Función:

- Realizar un **análisis** y crear un **punto de control** de todos los archivos, cifrándolos para aumentar su seguridad.
- **Monitorización** de cambios anómalos, comparándolos con el punto de referencia creado anteriormente, incluyendo fecha, hora, permisos, etc.

Este programa no solo se utiliza para detectar la integridad de los datos almacenados en un ordenador o máquina, sino que también es una herramienta para minimizar daños y el impacto de posibles intrusiones en el sistema. Tripwire proporciona un análisis detallado de los archivos modificados, facilitando su restauración en caso necesario.

Todos estos cambios realizados en el sistema deben ser notificados. Para ello, se envía un correo electrónico al administrador, asegurando que los datos no sean alterados o manipulados. Esto se logra mediante un proceso automático ejecutado a intervalos regulares de tiempo que podemos establecer, lo cual veremos a continuación.

### Instalación

En la instalación de este sistema en nuestro sistema Debian 12, deberemos seguir estos pasos:

1. Actualizar el sistema:

```bash
 		sudo apt update && apt upgrade - y
```

1. Instalar el programa en cuestión:

```bash
apt-get install tripwire
```

---

![image.png](Pra%CC%81ctica%20Herramientas%20de%20seguridad%201299a2c89a9380d1ac6bdb2d22b7bdab/image.png)

Durante la instalación, crearemos una clave de host y una contraseña de clave local.

![image.png](Pra%CC%81ctica%20Herramientas%20de%20seguridad%201299a2c89a9380d1ac6bdb2d22b7bdab/image%201.png)

![image.png](Pra%CC%81ctica%20Herramientas%20de%20seguridad%201299a2c89a9380d1ac6bdb2d22b7bdab/image%202.png)

![image.png](Pra%CC%81ctica%20Herramientas%20de%20seguridad%201299a2c89a9380d1ac6bdb2d22b7bdab/image%203.png)

![image.png](Pra%CC%81ctica%20Herramientas%20de%20seguridad%201299a2c89a9380d1ac6bdb2d22b7bdab/image%204.png)

![image.png](Pra%CC%81ctica%20Herramientas%20de%20seguridad%201299a2c89a9380d1ac6bdb2d22b7bdab/image%205.png)

![image.png](Pra%CC%81ctica%20Herramientas%20de%20seguridad%201299a2c89a9380d1ac6bdb2d22b7bdab/image%205.png)

![image.png](Pra%CC%81ctica%20Herramientas%20de%20seguridad%201299a2c89a9380d1ac6bdb2d22b7bdab/image%206.png)

> En caso de que las contraseñas no funcionen o que deseemos modificarlas para aumentar su seguridad, ejecutaremos el siguiente comando:
> 

```bash
sudo dpkg-reconfigure tripwire
```

1. Ahora lo que haremos será iniciar el servicio, y meter la contraseña que hemos configurado mediante la instalación:

```bash
sudo tripwire —init
```

![image.png](Pra%CC%81ctica%20Herramientas%20de%20seguridad%201299a2c89a9380d1ac6bdb2d22b7bdab/image%207.png)

Después de que acabe nos saldrá por pantalla lo siguiente:

![image.png](Pra%CC%81ctica%20Herramientas%20de%20seguridad%201299a2c89a9380d1ac6bdb2d22b7bdab/image%208.png)

1. Ahora modificaremos el archivo de configuración "twpol.txt" para descomentar las líneas que se refieren a los datos recopilados al iniciar el sistema:

Por lo que vamos a descomentar las siguientes lineas:

![image.png](Pra%CC%81ctica%20Herramientas%20de%20seguridad%201299a2c89a9380d1ac6bdb2d22b7bdab/image%209.png)

Esto debe de estar descomentado todo el fichero, ya que queremos una base de datos pero sobre todo, estas dos:

```bash
/root/.bashrc
/root/.bash_profile
```

1. Para que estos cambios se guarden se deberá usar:

```bash
sudo twadmin -m P /etc/tripwire/twpol.txt
```

![image.png](Pra%CC%81ctica%20Herramientas%20de%20seguridad%201299a2c89a9380d1ac6bdb2d22b7bdab/image%2010.png)

Como podemos ver, se han escrito los cambios correctamente , con lo que iniciaremos el tripwire

```bash
sudo tripwire —init 
```

![image.png](Pra%CC%81ctica%20Herramientas%20de%20seguridad%201299a2c89a9380d1ac6bdb2d22b7bdab/image%2011.png)

1. Verificación de los parámetros de Tripwire.

```bash
sudo tripwire - - check
```

![image.png](Pra%CC%81ctica%20Herramientas%20de%20seguridad%201299a2c89a9380d1ac6bdb2d22b7bdab/image%2012.png)

### Configuración

**Configuración inicial** 

Para realizar la configuración inicial tras instalar la herramienta, aunque ya vienen predefinidos ciertos valores por defecto, es recomendable configurarlo de acuerdo con las necesidades y requerimientos específicos de nuestro sistema. Los dos archivos que debemos modificar para este propósito son /etc/tripwire/twcfg.txt y /etc/tripwire/twpol.txt. Estos archivos indican la ubicación de los datos de comprobación.

**Configuración de twcfg.txt**

Lo primero que tendremos que hacer es entrar en el archivo de configuración:

```bash
andy@SAD-Practica-1:~$ cd /etc/tripwire/
andy@SAD-Practica-1:/etc/tripwire$ sudo nano twcfg.txt
```

El archivo de configuración tendrá este aspecto:

```bash
ROOT          =/usr/sbin
POLFILE       =/etc/tripwire/tw.pol
DBFILE        =/var/lib/tripwire/$(HOSTNAME).twd
REPORTFILE    =/var/lib/tripwire/report/$(HOSTNAME)-$(DATE).twr
SITEKEYFILE   =/etc/tripwire/site.key
LOCALKEYFILE  =/etc/tripwire/$(HOSTNAME)-local.key
EDITOR        =/usr/bin/editor
LATEPROMPTING =false
LOOSEDIRECTORYCHECKING =false
MAILNOVIOLATIONS =true
EMAILREPORTLEVEL =3
REPORTLEVEL   =3
SYSLOGREPORTING =true
MAILMETHOD    =SMTP
SMTPHOST      =localhost
SMTPPORT      =25
TEMPDIRECTORY =/tmp
```

Vamos a desglosar cada una de las líneas y explicar el significado de las variables que aparecen en este fichero. Estas variables se conocen como variables de configuración.

> Variables de configuración: son obligatorias, ya que si no se especifica ningún valor, Tripwire mostrará un mensaje de error y terminará su ejecución.
> 

| ***Variable*** | ***Valor por defecto*** | ***Descripción*** |
| --- | --- | --- |
| Root | /usr/bin | Ejecutables de Tripwire |
| Polfile | /etc/tripwire/tw.pol | Ubicación del archivo de políticas |
| Dbfile | /var/lib/tripwire/$(HOSTNAME).twd | Archivo de la base de datos |
| Reporfile | /var/lib/tripwire/report/$(HOSTNAME)-$(DATE).twr | Archivos de informes |
| Sitekeyfile | /etc/tripwire/site.key | Llave del sitio |
| Localkeyfile | /etc/tripwire/$(HOSTNAME)-local.key | Llave local |

> Variables de configuración opcionales: no es necesario especificarlas, ya que pueden adoptar valores predeterminados.
> 

| ***Variable*** | ***Valor por defecto*** | ***Descripción*** |
| --- | --- | --- |
| Editor | /bin/vi | Indica el editor que se ejecutará. |
| Lateprompting | `True` o `False` | Tiempo de espera para solicitar contraseña al usuario. |
| Loosedirectorycheckin | `True` o `False` | Informa de cambios al daemon de syslog. |
| Mailnoviolations | `True` o `False` | Emails periódicos aún sin intrusión en el sistema. |
| Emailreportleve | 3 (valores válidos de 0 a 4) | Nivel de detalle de informes enviados por email. |
| Reportlevel | 3 (valores válidos de 0 a 4) | Nivel de detalle de informes generados con twprint. |
| Mailmethod | SMTP o SENDMAIL | Protocolo de correo en uso. |
| Mailprogram | /usr/sbin/sendmail --oi --t | Programa de correo en uso. |
| SMTPHOST | localhost | Dirección del servidor SMTP. |
| SMTPPORT | 25 | Puerto del servidor SMTP. |
| TEMPDIRECTORY | /tmp | Directorio temporal en uso. |
| Syslogreporting | `True` o `False` | Informa de cambios al daemon de syslog. |

**Configuración de twpol.txt**

En esta ocasión, estamos examinando el fichero que contiene la política de los ficheros y directorios que esta herramienta supervisará. Esto incluye el nivel de revisión que les otorgaremos y los datos que se almacenarán en la base de datos que se generará.

Este será el fichero que configuraremos para que se nos envíen los informes por correo electrónico.

Está conformado por:

- Comentarios: Texto que comienza con "#".
- Directivas: Conjunto de instrucciones que determinan cómo se interpreta la política de Tripwire.
- Reglas: Establecen la rigurosidad de la verificación.
- Variables: Permiten al usuario definir cadenas que serán reemplazadas en el archivo especificado.

**Especificación Reglas**

Como mencionamos anteriormente, las reglas establecen el nivel de rigurosidad con el que Tripwire realizará la verificación de archivos y directorios. Es importante destacar que existen dos tipos de reglas:

- Normales: especifican las propiedades que serán evaluadas.
Las reglas normales siguen la siguiente sintaxis:

```bash
nom_objet -> msc_propiedades
```

Desglose de la regla: 

- **nom_objeto**: (nombre del objeto). No permite el uso de variables, pero sí admite variables de Tripwire. Esta regla define la ubicación completa del archivo y/o directorio a verificar.
- **msc_propiedades**: (máscara de propiedades). Aquí se especifican las propiedades que deben ser analizadas.

Cada objeto puede asociarse únicamente a una máscara de propiedades. Si un objeto tiene más de una máscara asignada, se producirá un error y Tripwire no llevará a cabo el análisis.

Las propiedades que se pueden verificar o ignorar son las siguientes:

```bash
Código | Propiedad
a | Acceso (fecha y hora)
b | Bloques usados
c | Creación/modificación de inodos (fecha y hora)
d | Id del dispositivo donde están los inodos
g | Id del grupo del fichero
i | Nº inodos
l | Aumento de tamaño fichero
m | Modificación (fecha y hora)
n | Nº enlaces
p | Permisos y bits de modo (fichero)
r | Id dispositivo apuntado por el inodo (solo para objetos dispositivos)
s | Tamaño fichero
t | Tipo fichero
u | Id dueño del fichero
C | Valor del CRC-32 del fichero
H | Valor de Haval del fichero
M | Valor MD5 del fichero
S | Valor SHA del fichero
```

- Excluidas: especifican los directorios y/o archivos que Tripwire debe omitir en su análisis. Solo cuentan con cuatro atributos, que son:

| ***rulename*** | ***Nombre de la regla (Hace más ameno su búsqueda)*** |
| --- | --- |
| emailto | Asocia uno o más emails para enviar los informes |
| severity | Nivel de severidad de una regla (Valor por defecto 0. De 0 a 1.000.000) |
| recurse | Especifica el análisis. -1 y 0 no analiza subdirectorios y ficheros internos. A partir de 1
hasta 1.000.000 se indica la profundidad de análisis. (Valor por defecto true) |

**Especificación Directivas
****Como mencioné anteriormente, hay un conjunto de órdenes que influyen en la interpretación de la política de Tripwire, y su uso está restringido a un número limitado y reducido de estas.

| section | designa las políticas específicas de un sistema operativo. |
| --- | --- |
| ifhost…else…endif | permite emplear condicionales y nombre de la máquina o maquinas (separados por ‘||’) |
| print | imprime texto estándar con el diagnóstico y la depuración |
| error | detiene la ejecución e imprime un mensaje de error |
| end | Indica el final del fichero de políticas. |

**Especificación de variables**

| Variable | Valor | Descripción |
| --- | --- | --- |
| ReadOnly | `+pinugtsdbmCM-rlacSH` | Archivos de solo lectura. |
| Dynamic | `+pinugtd-srlbamcCMSH` | Directorios y archivos que cambian dinámicamente. |
| Growing | `+pinugtdl-srbamcCMSH` | Archivos que solo deben incrementar su tamaño. |
| Device | `+pugsdr-intlbamcCMSH` | Dispositivos o archivos sin opción de apertura. |
| IgnoreAll | `-pinugtsdrlbamcCMSH` | Presencia o ausencia de archivos. |
| IgnoreNone | `+pinugtsdrbamcCMSH-l` | Activa todas las propiedades de posible comprobación. |

### Programación

Hasta ahora podemos concluir lo que hace esta herramienta, el cual es generar un punto de restauración para los archivos críticos, por lo que vamos a aprovechar su funcionalidad haciendola automática por lo que vamos a acceder por consola y meteremos lo siguiente:

```bash
contrab -e
```

Nos saldrá lo siguiente:

![image.png](Pra%CC%81ctica%20Herramientas%20de%20seguridad%201299a2c89a9380d1ac6bdb2d22b7bdab/image%2013.png)

Lo que vemos es la selección del editor, y nos da a elegir entre estos dos:

- **Nano** (opción 1): Es un editor de texto simple y fácil de usar. Si no tienes experiencia con editores de texto en la terminal, esta es la mejor opción.
- **Vim** (opción 2): Es un editor más avanzado, pero puede ser un poco complicado si no estás familiarizado con él.

Obviamente elegimos el 1, y nos saldrá esto por pantalla:

![image.png](Pra%CC%81ctica%20Herramientas%20de%20seguridad%201299a2c89a9380d1ac6bdb2d22b7bdab/image%2014.png)

Como vemos en la línea final, se nos indica los parámetros necesarios para su automatización. En nuestro caso, lo haremos a través de un mail que introduciremos en el fichero de politicas para que nos envíen los reportes, de la siguiente manera:

![image.png](Pra%CC%81ctica%20Herramientas%20de%20seguridad%201299a2c89a9380d1ac6bdb2d22b7bdab/image%2015.png)

Y verificaremos después de salir del editor con el siguiente comando:

```bash
sudo contrab -l

```

Lo que nos saldrá por la terminal lo siguiente:

![image.png](Pra%CC%81ctica%20Herramientas%20de%20seguridad%201299a2c89a9380d1ac6bdb2d22b7bdab/image%2016.png)

Y como podemos ver esto nos muestra todas las taras programadas en el **contrab** para el usuario root.

### Alertas por correo

En la sección de introducción, mencionamos que se puede configurar Tripwire para que envíe correos electrónicos a uno o varios usuarios si alguna de las reglas definidas en el archivo de políticas ha sido modificada o infringida. Para lograr esto, debemos incluir una línea con la directiva correspondiente en ese mismo archivo.

Para esto , en ese fichero, le añadiremos la siguiente línea con esta directriz:

```bash
emailto = <email>[;<otro-email>]
```

El comando para entrar:

```bash
andy@SAD-Practica-1:~$ sudo nano /etc/tripwire/twpol.txt 
```

Y como se vería lo que hemos tocado, en este fichero:

```bash
# Tripwire Binaries
#
(
rulename = "Tripwire Binaries",
severity = $(SIG_HI)
emailto  = [asirandyglez@gmail.com](mailto:asirandyglez@gmail.com)
)
{
$(TWBIN)/siggen                 -> $(SEC_BIN) ;
$(TWBIN)/tripwire               -> $(SEC_BIN) ;
$(TWBIN)/twadmin                -> $(SEC_BIN) ;
$(TWBIN)/twprint                -> $(SEC_BIN) ;
}
```

Una vez que hemos realizado estos cambios, generaremos un nuevo archivo de políticas. Si querremos comprobar que la configuración de los avisos esta operativo, podemos comprobarlo con lo siguiente:

```bash
sudo /usr/sbin/tripwire -m t -e <email>
```

Esto nos enviará un mail de prueba al mail en cuestión, pero si tenemos un Gmail, como es mi caso, tendremos que preparar nuestro Gmail.

Aquí tenemos la comprobación:

```bash
andy@SAD-Practica-1:~$ /usr/sbin/tripwire -m t -e [asirandy@gmail.com](mailto:asirandy@gmail.com)
Sending a test message to: [asirandy@gmail.com](mailto:asirandy@gmail.com)
```

### Preparación de Gmail

Google desde el año 2021 corto el tráfico de mensajes de apps a sus correos, porque le vamos a habilitare con una serie de configuraciones previas.

Para ello tendremos que ir a nuestra de Gmail e ir al apartado de ***Gestionar tu cuenta de Google.***

![image.png](Pra%CC%81ctica%20Herramientas%20de%20seguridad%201299a2c89a9380d1ac6bdb2d22b7bdab/image%2017.png)

Una vez dentro tendremos que irnos al margen izquierdo y buscar la pestaña que pone seguridad:

![image.png](Pra%CC%81ctica%20Herramientas%20de%20seguridad%201299a2c89a9380d1ac6bdb2d22b7bdab/image%2018.png)

Ahora tendremos que mirar hacia abajo o más bien mover la barra lateral hacia abajo y tendremos que tener habilitada la verificación en dos pasos:

![image.png](Pra%CC%81ctica%20Herramientas%20de%20seguridad%201299a2c89a9380d1ac6bdb2d22b7bdab/image%2019.png)

Una vez hecho esto, dentro tendremos que buscar Contraseñas de aplicación, en mi caso no se encuentra, pero os dejo un link que os lleva directamente, una vez tengáis la verificación en dos pasos:

```bash
[https://myaccount.google.com/apppasswords?pli=1&rapt=AEjHL4PVBeRvsoo4g3FPzMcG7S70E7TNZ8V9I1m44HphLc1_cxMb-HY2HCDQyE04YkeWNGmAEvBXJg9Cd8-wZjYCQdjviHKGA-h_tSJHuzp1MmZwhnzQFSg](https://myaccount.google.com/apppasswords?pli=1&rapt=AEjHL4PVBeRvsoo4g3FPzMcG7S70E7TNZ8V9I1m44HphLc1_cxMb-HY2HCDQyE04YkeWNGmAEvBXJg9Cd8-wZjYCQdjviHKGA-h_tSJHuzp1MmZwhnzQFSg)
```

Una vez hayáis llegado hasta aquí lo único que tendréis que hacer es escribir el nombre de la aplicación para que se os genere una contraseña, de la siguiente manera:

![image.png](Pra%CC%81ctica%20Herramientas%20de%20seguridad%201299a2c89a9380d1ac6bdb2d22b7bdab/image%2020.png)

![image.png](Pra%CC%81ctica%20Herramientas%20de%20seguridad%201299a2c89a9380d1ac6bdb2d22b7bdab/image%2021.png)

Una vez hecho esto pasaremos a la configuración de la máquina.

### Configuración de la máquina para activar las alertas por correos electrónico

Para que nos puedan mandar correos electrónicos de informes realizados a través de la consola de comandos, debemos instalar en el sistema **postfix** y **mailutils**. 

Lo haremos con lo siguientes pasos:

1. Actualizar el sistema

```bash
apt update && apt upgrade -y
```

1. Instalar postfix y mailutils

```bash
apt-get install postfix mailutils -y
```

En la instalación saldrá la siguiente pantalla:

![image.png](Pra%CC%81ctica%20Herramientas%20de%20seguridad%201299a2c89a9380d1ac6bdb2d22b7bdab/image%2022.png)

La cual tendréis que elegir **Internet Site** y darle a aceptar en la siguiente.

1. Crearemos el fichero **/etc/postfix/sasl_passwd** y escribiremos lo siguiente:

```bash
[[smtp.gmail.com](http://smtp.gmail.com/)]:587 asirandyglez[@gmail.com](mailto:mariajesus.allozarodriguez@gmail.com):genereted_pass
```

En este caso como mi cuenta de mail es gmail, debemos poner el puerto **587** y smtp, que el protocolo que vamos a emplear para enviar correos desde nuestra consola de comandos a nuestro correo. 

Os pongo aquí los distintos puertos para el Hotmail, que serian el puerto **smtp 465 o bien el 25.**

En el lugar de **genereted_pass** vamos a introducir la contraseña que hemos generado en el
apartado anterior.

Una vez efectuados los cambios, cambiamos los permisos del fichero con **chmod 600
/etc/postfix/sasl_passwd.**

1. Abrimos el fichero de configuración de postfix, donde están configuradas las directrices para que todo correo saliente, se envíe por el servidor STMP de Google y nos identifique como usuarios.

```bash
sudo nano /etc/postfitx/main.cf
Y este fichero tendra que tener este formato:
relayhost = [smtp.gmail.com]:587
mydestination = localhost.localdomain, localhost
smtp_sasl_auth_enable = yes
smtp_sasl_security_options =
smtp_sasl_password_maps = hash:/etc/postfix/sasl/sasl_passwd
smtp_tls_security_level = encrypt
smtp_tls_CAfile = /etc/ssl/certs/ca-certificates.crt
```

> Si os esta dando ruido este es el que funciona, solo tendríais que sustituir vuestro [main.cf](http://main.cf) y meter este, y ya seria solo cuestión de que cambiéis vuestros datos (mydestination, myhostaname):
> 

```bash
andy@SAD-Practica-1:/etc/postfix$ cat main.cf
# Debian specific:  Specifying a file name will cause the first
# line of that file to be used as the name.  The Debian default
# is /etc/mailname.
# myorigin = /etc/mailname

smtpd_banner = $myhostname ESMTP $mail_name (Debian/GNU)
biff = no
append_dot_mydomain = no
readme_directory = no
compatibility_level = 3.6

# TLS parameters
smtpd_tls_cert_file=/etc/ssl/certs/ssl-cert-snakeoil.pem
smtpd_tls_key_file=/etc/ssl/private/ssl-cert-snakeoil.key
smtpd_tls_security_level=may

smtp_tls_CApath=/etc/ssl/certs
smtp_tls_security_level=encrypt
smtp_tls_CAfile=/etc/ssl/certs/ca-certificates.crt
smtp_tls_session_cache_database = btree:${data_directory}/smtp_scache

smtpd_relay_restrictions = permit_mynetworks permit_sasl_authenticated defer_unauth_destination
myhostname = SAD-practica-1
alias_maps = hash:/etc/aliases
alias_database = hash:/etc/aliases
mydestination = SAD-practica-1, localhost.localdomain, localhost
relayhost = [smtp.gmail.com]:587
mynetworks = 127.0.0.0/8 [::ffff:127.0.0.0]/104 [::1]/128
mailbox_size_limit = 600000
recipient_delimiter = +
inet_interfaces = all
inet_protocols = all

# Configuración de SASL
smtp_sasl_auth_enable = yes
smtp_sasl_security_options = noanonymous
smtp_sasl_password_maps = hash:/etc/postfix/sasl_passwd

```

Y ya solamente quedaría compilar los cambios con postmap, reiniciar el servicio y comprobar que recibimos correos de la herramienta en nuestro mail.

```bash
sudo postmap /etc/postfix/sasl_passwd
sudo systemctl restart postfix
```

Por lo que haremos el siguiente comando para ver si Tripwire funciona correctamente:

```bash
root@SAD-Practica-1:/etc/tripwire# /usr/sbin/tripwire -m t -e [asirandyglez@gmail.com](mailto:asirandyglez@gmail.com)
Sending a test message to: [asirandyglez@gmail.com](mailto:asirandyglez@gmail.com)
```

Y esto nos hará llegar un mail, como este:

![image.png](Pra%CC%81ctica%20Herramientas%20de%20seguridad%201299a2c89a9380d1ac6bdb2d22b7bdab/image%2023.png)

y ahora enviamos el check que hicimos antes con el siguiente comando:

```bash
sudo tripwire --check | sendmail -v [asirandyglez@gmail.com](mailto:asirandyglez@gmail.com)
```

y se nos envía al mail de la siguiente manera:

![Captura desde 2024-10-18 17-11-57.png](Pra%CC%81ctica%20Herramientas%20de%20seguridad%201299a2c89a9380d1ac6bdb2d22b7bdab/Captura_desde_2024-10-18_17-11-57.png)

![image.png](Pra%CC%81ctica%20Herramientas%20de%20seguridad%201299a2c89a9380d1ac6bdb2d22b7bdab/image%2024.png)

### Actualización automática

Para tener una actualización automática, lo que tendremos que hacer es un script:

```bash
#!/bin/sh -e

tripwire=/usr/sbin/tripwire

# Comprueba si Tripwire existe
[ -x "$tripwire" ] || exit 0

# Establecer umask para la creación de archivos
umask 027

# Ejecutar Tripwire con la opción --check y redirigir la salida a sendmail
$tripwire --check --quiet | sendmail -v asirandyglez@gmail.com || exit 0
```

Este script almacenado en **/etc/cron.daily/tripware** le daremos los siguientes permisos:

```bash
chmod 755 /etc/cron.daily/tripwire
```

Verificación:

```bash
andy@SAD-Practica-1:~$ cd /etc/cron.daily/
andy@SAD-Practica-1:/etc/cron.daily$ ls
apt-compat  dpkg  exim4-base  logrotate  man-db  sysstat  tripwire
andy@SAD-Practica-1:/etc/cron.daily$ cd tripware
-bash: cd: tripware: No existe el fichero o el directorio
andy@SAD-Practica-1:/etc/cron.daily$ sudo nano tripware
[sudo] contraseña para andy:
andy@SAD-Practica-1:/etc/cron.daily$ chmod 755 /etc/cron.daily/tripwire
chmod: cambiando los permisos de '/etc/cron.daily/tripwire': Operación no permitida
andy@SAD-Practica-1:/etc/cron.daily$ sudo chmod 755 /etc/cron.daily/tripwire
andy@SAD-Practica-1:/etc/cron.daily$
```

## Rkhunter

Rkhunter es una herramienta para la detección de rootkits. 

Primeramente, nos tendremos que hacer la siguiente pregunta:

**¿Qué son exactamente los rootkits?**

E primer paso es saber de donde viene esté término,el cual proviene de las palabras inglesas *root* (raíz) y *kit* (conjunto de herramientas). 

Los rootkits son programas maliciosos diseñados para operar de forma encubierta, ocultando procesos, programas, archivos, directorios, claves de registro y puertos. Esto permite a un intruso mantener acceso no autorizado a diversos sistemas operativos, como GNU/Linux, Solaris o Microsoft Windows. Con ese acceso privilegiado, el atacante puede ejecutar, instalar, modificar aplicaciones o extraer información sensible de manera remota, comprometiendo la seguridad del sistema.

Ahora que entendemos el riesgo, veamos cómo protegernos de esta amenaza.

### Instalación

Para instalar esta herramienta en Debian 12, tendremos que seguir los siguientes pasos:

1. Actualizar el sistema

```bash
sudo apt update && apt upgrade -y
```

1. Instalación del paquete Rkhunter

```bash
sudo apt install rkhunter -y 
```

![image.png](Pra%CC%81ctica%20Herramientas%20de%20seguridad%201299a2c89a9380d1ac6bdb2d22b7bdab/image%2025.png)

### Configuración

Lo primero que debemos saber es que RKHunter tiene un archivo de configuración donde puedes ajustar varias directivas y parámetros que vienen predefinidos. A continuación, os voy a mostrar cómo se accede a este archivo y qué opciones podemos modificar.

Desde ahí, podemos configurar cosas como la frecuencia con la que se actualiza la base de datos de RKHunter, o incluso establecer una dirección de correo electrónico donde recibiremos los informes con los resultados de los análisis del sistema.

### Archivo de ubicación

El archivo de configuración esta ubicado en **`*/etc/rkhunter.conf*`** por lo que necesitaremos permisos de root por lo que vamos aponer el siguiente comando:

```bash
sudo nano /etc/rkhunter.conf
```

![image.png](Pra%CC%81ctica%20Herramientas%20de%20seguridad%201299a2c89a9380d1ac6bdb2d22b7bdab/image%2026.png)

Las configuraciones de RKHunter se pueden realizar de dos maneras: 

- Modificando directamente el archivo de configuración principal.
- Creando un archivo de configuración local personalizado.
    - Este archivo debe llamarse `*rkhunter.conf.local*` y debe estar ubicado en la misma ruta que el archivo original.

 También esta la opción de crear un directorio llamado `*rkhunter.d*` dentro de `*/etc*` y guardar allí varios archivos de configuración, sin restricción de nombres, siempre que terminen en `*.conf*`.

Una vez que hayamos realizado los cambios en cualquiera de estos archivos de configuración, es recomendable ejecutar un comando específico en la consola para que las modificaciones tengan efecto.

```bash
sudo rkhunter -c
```

### Opciones de configuración del comando rkhunter

Con el comando anterior, existen muchos parámetros que se pueden modificar, los cuales vamos a mostrar a continuación:

### Configuración de mirrors.

Esta configuración afecta la forma en que RKHunter maneja las actualizaciones desde los  servidores que almacenan las actualizaciones ( "espejos"). 

Si configuramos la opción en "0", RKHunter intentará conectarse a los espejos en el orden de prioridad. Si el primero falla, intentará con el siguiente, y así sucesivamente hasta que uno funcione.

Por otro lado, si ponemos la opción `*ROTATE_MIRRORS*` en "**1**", RKHunter cambiará entre diferentes espejos de manera automática cada vez que use las opciones de actualización (`*-update*`) o verificación de versiones (`*-versioncheck*`). Ya que esto ayuda a repartir la carga entre varios servidores, evitando que uno solo se sobrecargue.

![image.png](Pra%CC%81ctica%20Herramientas%20de%20seguridad%201299a2c89a9380d1ac6bdb2d22b7bdab/image%2027.png)

### Configuración y verificación de actualizaciones en mirrors

Para verificar manualmente las actualizaciones, debemos configurar la opción `*ROTATE_MIRRORS*` en "`0`". Esto es útil en servidores locales, ya que permite controlar qué servidor espejo (o "mirror") se utiliza de manera más directa, sin rotar entre varios.

Si en cambio configuramos la variable en "`1`", cuando usemos la opción `*-update*`, RKHunter verificará automáticamente los servidores espejo de forma rotativa, asegurándose de que el archivo de actualización se descargue desde un servidor disponible, lo que ayuda a equilibrar la carga entre diferentes espejos.

![image.png](Pra%CC%81ctica%20Herramientas%20de%20seguridad%201299a2c89a9380d1ac6bdb2d22b7bdab/image%2028.png)

### Configuración de avisos por mail

Como hemos visto con la herramienta Tripries, también tenemos la posibilidad de poder enviar un mail si se encuentra alguna alerta cuando se realiza la comprobación del sistema.

En esta herramienta al igual que pasa con Tripiwre podemos poner una o varias cuentas de mail.

Esta es la linea, que tendríamos que descomentar:

![image.png](Pra%CC%81ctica%20Herramientas%20de%20seguridad%201299a2c89a9380d1ac6bdb2d22b7bdab/image%2029.png)

E insertar el mail en cuestión:

![image.png](Pra%CC%81ctica%20Herramientas%20de%20seguridad%201299a2c89a9380d1ac6bdb2d22b7bdab/image%2030.png)

Nos aseguramos que la línea de MAIL_CMD, tenga la siguiente forma:

![image.png](Pra%CC%81ctica%20Herramientas%20de%20seguridad%201299a2c89a9380d1ac6bdb2d22b7bdab/image%2031.png)

Para que nos llegue el mail, tendremos que hacer los isguientes pasos:

1. Instalar sendmail

```powershell
sudo apt-get install sendmail -y
```

1. Editar el archivo de configuración /etc/mail para poder trabar con los servidores de Gmail, para eso añadiremos lo siguiente:

```bash
define(SMART_HOST', [smtp.gmail.com](http://smtp.gmail.com/)')dnl
define(RELAY_MAILER_ARGS', TCP $h 587')dnl
define(ESMTP_MAILER_ARGS', TCP $h 587')dnl
FEATURE(authinfo',hash -o /etc/mail/authinfo.db')dnl
```

Comprobación:

![image.png](Pra%CC%81ctica%20Herramientas%20de%20seguridad%201299a2c89a9380d1ac6bdb2d22b7bdab/image%2032.png)

Al igual que en Tripwire he hecho una contraseña generada:

![image.png](Pra%CC%81ctica%20Herramientas%20de%20seguridad%201299a2c89a9380d1ac6bdb2d22b7bdab/image%2033.png)

Y la he puesto en este fichero que acabo de crear:

`sudo nano /etc/mail/authinfo`

Y he metido lo siguiente:

`AuthInfo:smtp.gmail.com "U:root" "[I:tu_correo@gmail.com](mailto:I:tu_correo@gmail.com)" "P:contraseña_generada" "M:PLAIN"`

Ahora  tendremos que hacer lo siguiente:

1. Compilar el archivo de configuración:

```bash
root@SAD-Practica-1:/home/andy# sudo makemap hash /etc/mail/authinfo < /etc/mail/authinfo
```

1. Compilar el archivo de `sendmail.mc`

```bash
sudo cat /etc/mail/authinfo | sudo makemap hash /etc/mail/authinfo
```

1. Reiniciar el servicio de `sendmail`

```bash
sudo service sendmail restart
```

1. Prueba de que podemos enviar un mail:

```bash
echo "Hola holita vecinito es un correo de prueba de RKHunter" | sudo sendmail -t [asirandyglez@gmail.com](mailto:asirandygmail.com@gmail.com)
```

Y como podemos ver ya recibimos desde RKHunter:

![image.png](Pra%CC%81ctica%20Herramientas%20de%20seguridad%201299a2c89a9380d1ac6bdb2d22b7bdab/image%2034.png)

### Actualizaciones

En esta sección, exploraremos varias formas de realizar actualizaciones para mantener nuestro sistema libre de cualquier "infección" o "software no deseado" que podríamos haber pasado por alto.

**Comprobación de la versión instalada y disponible**

Para asegurar una protección efectiva de nuestro sistema, es fundamental mantener nuestra herramienta actualizada con la versión más reciente. Para ello, es importante utilizar dos comandos que nos ayudarán en el proceso de actualización.

Lo primero que haremos será verificar es la versión en la que esta nuestro sistema:

```bash
sudo rkhunter --version
```

![image.png](Pra%CC%81ctica%20Herramientas%20de%20seguridad%201299a2c89a9380d1ac6bdb2d22b7bdab/image%2035.png)

Hay  otro comando con el que podemos verificar la versión que tenemos instalada con la ultima que esta disponible (dos en uno). En caso de no ser así, lo actualizamos de normal con los repositorios que tenemos en nuestra distribución.

```bash
sudo rkhunter —versioncheck
```

Este comando nos dará el siguiente error:

```bash
andy@SAD-Practica-1:~$ sudo rkhunter --versioncheck
Invalid WEB_CMD configuration option: Relative pathname: "/bin/false"
```

Por lo que tendremos que tocar el fichero de configuración, y buscar la siguiente linea y descomentarla:

```bash
WEB_CMD= curl 
```

![image.png](Pra%CC%81ctica%20Herramientas%20de%20seguridad%201299a2c89a9380d1ac6bdb2d22b7bdab/image%2036.png)

Y ahora comprobaríamos con el comando de la versión:

```bash
sudo rkhunter — version
```

![image.png](Pra%CC%81ctica%20Herramientas%20de%20seguridad%201299a2c89a9380d1ac6bdb2d22b7bdab/image%2037.png)

Esto que estamos viendo por pantalla nos va a dar error, por lo que tendremos que meternos en el fichero de configuración y cambiar lo siguiente en las lineas siguientes:

```
MIRRORS_MODE=1 ---> MIRRORS_MODE=0

UPDATE_MIRRORS=0 ---> UPDATE_MIRRORS=1

WEB_CMD="/bin/false" ---> #WEB_CMD=""
```

Por lo que ahora si hacemos un  `- -versioncheck`

![image.png](Pra%CC%81ctica%20Herramientas%20de%20seguridad%201299a2c89a9380d1ac6bdb2d22b7bdab/image%2038.png)

### Actualizar configuraciones de Rkhunter

Cuando realizamos cualquier cambio en nuestros ficheros de configuración, para verificar que los cambios han sido efectivos, ejecutaremos el siguiente comando:

```bash
sudo rkhunter -C
```

Si no obtenemos salida, significar que ha hemos tenido éxito.

![image.png](Pra%CC%81ctica%20Herramientas%20de%20seguridad%201299a2c89a9380d1ac6bdb2d22b7bdab/image%2039.png)

### Actualizar los ficheros de las bases de datos

Es muy importante es tener nuestros ficheros de las bases de datos actualizados, para eso debemos de tener en cuenta distintos niveles de actualización.
Por eso voy a poner ciertos comandos muy útiles:

```bash
sudo rkhunter - - update
```

![image.png](Pra%CC%81ctica%20Herramientas%20de%20seguridad%201299a2c89a9380d1ac6bdb2d22b7bdab/image%2040.png)

Esto que acabamos de ver no es ningún comando de actualización, ya que solo actualiza como he indicado con anterioridad los ficheros de la base de datos, la cual incluyendo la del idioma.

La siguiente forma de actualización es la de actualizar todas las bases de datos de propiedades de ficheros. El cual es el  siguiente paso que se hace después de haber ejecutado el comado anterior:

```bash
sudo rkhunter —propupd
```

![image.png](Pra%CC%81ctica%20Herramientas%20de%20seguridad%201299a2c89a9380d1ac6bdb2d22b7bdab/image%2041.png)

Por favor actualizar previamente , aunque tengamos las actualizaciones automáticas.

### Opciones del comando rkhunter

En este apartado lo que veremos son las distintas opciones de comandos, para eso podemos ayudarnos de la ayuda misma de lo que es RKHunter, con el siguiente comando:

```bash
sudo rkhunter — help
```

```bash
Usage: rkhunter  {--check | --unlock | --update | --versioncheck |
									--propupd [{filename | directory | package name},...] |
									--list [{tests | {lang | languages} | rootkits | perl | propfiles}] |
									--config-check | --version | --help} [options]
									
```

| Opción | Descripción |
| --- | --- |
| `--append-log` | Append to the logfile, do not overwrite |
| `--bindir <directory>...` | Use the specified command directories |
| `-c, --check` | Check the local system |
| `-C, --config-check` | Check the configuration file(s), then exit |
| `--cs2, --color-set2` | Use the second color set for output |
| `--configfile <file>` | Use the specified configuration file |
| `--cronjob` | Run as a cron job (implies -c, --sk and --nocolors options) |
| `--dbdir <directory>` | Use the specified database directory |
| `--debug` | Debug mode (Do not use unless asked to do so) |
| `--disable <test>[,<test>...]` | Disable specific tests (Default is to disable no tests) |
| `--display-logfile` | Display the logfile at the end |
| `--enable <test>[,<test>...]` | Enable specific tests (Default is to enable all tests) |
| `--hash {MD5` | SHA1 |
| `-h, --help` | Display this help menu, then exit |
| `--lang, --language <language>` | Specify the language to use (Default is English) |
| `--list [tests` | languages |
| `-l, --logfile [file]` | Write to a logfile (Default is /var/log/rkhunter.log) |
| `--noappend-log` | Do not append to the logfile, overwrite it |
| `--nocf` | Do not use the configuration file entries for disabled tests (only valid with --disable) |
| `--nocolors` | Use black and white output |
| `--nolog` | Do not write to a logfile |
| `--nomow, --no-mail-on-warning` | Do not send a message if warnings occur |
| `--ns, --nosummary` | Do not show the summary of check results |
| `--novl, --no-verbose-logging` | No verbose logging |
| `--pkgmgr {RPM` | DPKG |
| `--propupd [file` | directory |
| `-q, --quiet` | Quiet mode (no output at all) |
| `--rwo, --report-warnings-only` | Show only warning messages |
| `--sk, --skip-keypress` | Don't wait for a keypress after each test |
| `--summary` | Show the summary of system check results (This is the default) |
| `--syslog [facility.priority]` | Log the check start and finish times to syslog (Default level is authpriv.notice) |
| `--tmpdir <directory>` | Use the specified temporary directory |
| `--unlock` | Unlock (remove) the lock file |
| `--update` | Check for updates to database files |
| `--vl, --verbose-logging` | Use verbose logging (on by default) |
| `-V, --version` | Display the version number, then exit |
| `--versioncheck` | Check for latest version of program |
| `-x, --autox` | Automatically detect if X is in use |
| `-X, --no-autox` | Do not automatically detect if X is in use |

### Escaneo del sistema

Para que podamos hacer un escaneo de nuestro sistema de una forma completa, lo podremos hacer de dos formas distintas:

```bash
sudo rkhunter -C
sudo rkhunter —check
```

Esto nos mostrará por pantalla lo siguiente:

![image.png](Pra%CC%81ctica%20Herramientas%20de%20seguridad%201299a2c89a9380d1ac6bdb2d22b7bdab/image%2042.png)

Llegados a esta parte, podríamos considerarla como la primera parte del análisis, el cual tendremos que darle a **ENTER** y la herramienta analizará por etapas nuestro sistema.

Rootkit será la siguiente búsqueda:

![image.png](Pra%CC%81ctica%20Herramientas%20de%20seguridad%201299a2c89a9380d1ac6bdb2d22b7bdab/image%2043.png)

Al finalizar tenemos que confirmar nuevamente al a siguiente etapa, que es la de escaneos de los ficheros y módulos del kernel en busca de malware, rookits y backdoors.

![image.png](Pra%CC%81ctica%20Herramientas%20de%20seguridad%201299a2c89a9380d1ac6bdb2d22b7bdab/image%2044.png)

Volvemos a confirmar y esta vez examinara el [localhost](http://localhost) y redes:

![image.png](Pra%CC%81ctica%20Herramientas%20de%20seguridad%201299a2c89a9380d1ac6bdb2d22b7bdab/image%2045.png)

En esta etapa nos ha localizado un warning dado que en el fichero de
`/etc/ssh/sshd_config` tengo configurada la línea PermitRootLogin no. Para que no nos
vuelva a saltar dicho warning debemos de configurarlo de la siguiente manera:
En `/etc/ssh/sshd_config` ponemos:

```bash
PermitRootLogin without-password
```

y en `/etc/rkhunter.conf`

```bash
ALLOW_SSH_ROOT_USER=without-password
```

Y el ultimo <ENTER> nos lleva al resultado de la búsqueda total:

![image.png](Pra%CC%81ctica%20Herramientas%20de%20seguridad%201299a2c89a9380d1ac6bdb2d22b7bdab/image%2046.png)

Al finalizar nuestro análisis, se nos mandará un correo electrónico, que previamente hemos
configurado para recibir las alertas del sistema:

![image.png](Pra%CC%81ctica%20Herramientas%20de%20seguridad%201299a2c89a9380d1ac6bdb2d22b7bdab/image%2047.png)

# Pablo Martín - Alumno 4

## **Introducción**

Hoy en día, vivimos en un mundo cada vez más conectado, donde gran parte de nuestras actividades cotidianas, desde el acceso a redes sociales hasta operaciones bancarias, se realizan de manera digital. Sin embargo, a pesar de la creciente dependencia de la tecnología, muchas personas todavía no le dan la importancia necesaria a la seguridad de sus contraseñas. Esto es un error que puede tener consecuencias graves.

El uso de contraseñas débiles y predecibles, como "123456" o "contraseña", sigue siendo demasiado común. Muchos usuarios optan por estas combinaciones fáciles de recordar sin considerar los riesgos a los que se exponen. En un entorno donde los ciberataques son cada vez más frecuentes y sofisticados, los atacantes malintencionados aprovechan cualquier vulnerabilidad para acceder a información personal y confidencial, realizar fraudes o incluso dañar la reputación de una persona o empresa.

Los **crackers**, personas que buscan vulnerar sistemas con fines maliciosos, cuentan con herramientas avanzadas que pueden descifrar contraseñas en cuestión de minutos si no se siguen las mejores prácticas de seguridad. Es por eso que utilizar contraseñas fuertes, únicas y gestionarlas adecuadamente se ha convertido en un requisito esencial para proteger nuestra identidad digital.

En esta práctica, exploraremos diversas herramientas que nos ayudarán a comprender mejor cómo podemos mejorar la fortaleza de nuestras contraseñas, garantizando una mayor seguridad en nuestras cuentas y protegiéndonos frente a las amenazas constantes que acechan en la red.

### **Herramientas Online**

Las herramientas online de verificación de contraseñas son servicios basados en la web que evalúan la seguridad de una contraseña proporcionada, realizando análisis como la longitud, la combinación de caracteres (mayúsculas, minúsculas, números, símbolos), y verificando si esa contraseña ha sido expuesta en bases de datos filtradas.

Por ejemplo, voy a comprobar la seguridad de una contraseña típica como “user” en una herramienta como [Password Kaspersky](https://password.kaspersky.com/es/):

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXfxWoOAoK-cQwsXN1j98Brksk3PgrhflRCDwma-uh5Eeb0TDYF7qOcEBoTUwR5lukf_McBvDlaFAOAxmVRlVWiL0G4onbQttlM41xJ7MieRjdiAMoG35WnB8_baE2HtXTWvu1SxkrHSMWSsrc6RHttkpJw?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfxWoOAoK-cQwsXN1j98Brksk3PgrhflRCDwma-uh5Eeb0TDYF7qOcEBoTUwR5lukf_McBvDlaFAOAxmVRlVWiL0G4onbQttlM41xJ7MieRjdiAMoG35WnB8_baE2HtXTWvu1SxkrHSMWSsrc6RHttkpJw?key=amEUHfTdJnvQeZF3EjeoeA)

Como podemos observar es una contraseña muy fácil de crackear, pues se encuentra registrada **267.110** veces en bases de datos de contraseñas filtradas.

Voy a generar algunas contraseñas y verificarlas en el comprobador, además realizaré una simulación en donde me registraré en alguna página con una contraseña segura generada por una herramienta. Pero antes voy a explicar lo que debemos hacer para mantener  la seguridad de una contraseña:

1. Usar una contraseña diferente para cada sitio. Debemos ser conscientes de que utilizar la misma clave para múltiples cuentas nos expone a grandes riesgos. Si un ciberdelincuente logra descifrar nuestra contraseña en una plataforma, también tendrá acceso a todos nuestros perfiles que comparten esa misma clave. Por lo que para fortalecer nuestra protección, es importante que generemos contraseñas únicas y aleatorias para cada servicio que utilicemos.
2. Usar un generador de contraseñas para crear contraseñas seguras. Cuando creamos nuestras contraseñas, debemos asegurarnos de que sean imposibles de descifrar. Es importante que las hagamos lo suficientemente largas, con un mínimo de 16 caracteres. Evitemos incluir palabras que se puedan encontrar en un diccionario o usar sustituciones de símbolos que sean obvias, cómo reemplazar la 'a' por '@'. También es importante que nos abstengamos de incorporar información personal que pueda ser fácilmente adivinada, como nuestras fechas de nacimiento o los nombres de nuestras mascotas, amigos y familiares. Siguiendo estas pautas, estaremos creando contraseñas mucho más seguras y difíciles de vulnerar.
3. Guardar nuestras contraseñas en un administrador de contraseñas. Si vamos a usar contraseñas seguras, necesitaremos que alguien las guarde. Porque como es obvio, si poniendo contraseñas simbólicas no nos acordamos la mayoría de las veces, con este tipo de contraseñas va a ser tarea imposible.
4. Actualizar las contraseñas cuando sea necesario. Si por alguna razón creemos que nuestra contraseña ha sido expuesta, por ejemplo, si recibimos una notificación de una posible violación. En ese caso, debemos actualizar nuestra contraseña para quedarnos más tranquilos.

Adjunto imagen real de una brecha de seguridad de mis contraseñas:

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXdd7yJNvd9fUWgHoWqZAKo5p2QA6HbfxElPhu6U2NIVQNUil9rNYTB9QNDgFIHxP4YwbJyH0SI9wV9d7Q7UVUXeIKAkdlXAIyj1SAVmJGm_fYzUPt63zjRMU3qQ1dIeyrhK0G9sdhmC520S9kAYJytYpPdZ?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdd7yJNvd9fUWgHoWqZAKo5p2QA6HbfxElPhu6U2NIVQNUil9rNYTB9QNDgFIHxP4YwbJyH0SI9wV9d7Q7UVUXeIKAkdlXAIyj1SAVmJGm_fYzUPt63zjRMU3qQ1dIeyrhK0G9sdhmC520S9kAYJytYpPdZ?key=amEUHfTdJnvQeZF3EjeoeA)

Una vez explicado, voy a crear una contraseña con una herramienta online. Existen muchas de ellas, yo me he decantado por [RoboForm](https://www.roboform.com/es/password-generator).

Para crearla es tan simple como dirigirnos a la página y modificar los parámetros a nuestra elección, aunque cuanto más difícil, mejor.

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXdru_n1cRWxFcWUkXpXIitMH6SbVw7S_n38Zw6bsn8x4GR1m1qBJyWThEYOzctcGRw3OINR7FPTsj6KWMJeX7qWs6JWWHFy1yV57Beep66hugL7nSYiRgfVRmMdI5Jzn42MIuMLbcXipIRdlkSj1ekSCtR7?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdru_n1cRWxFcWUkXpXIitMH6SbVw7S_n38Zw6bsn8x4GR1m1qBJyWThEYOzctcGRw3OINR7FPTsj6KWMJeX7qWs6JWWHFy1yV57Beep66hugL7nSYiRgfVRmMdI5Jzn42MIuMLbcXipIRdlkSj1ekSCtR7?key=amEUHfTdJnvQeZF3EjeoeA)

Copiamos la contraseña y verificamos que tan segura es:

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXfSoWkIExAq9X-2fUkT8TsJVt2GLoh6VzN3f7dCV9PbAAnrxmYGmoFgo_w3nRa4W723WthfWi4tDANgSf-0Jts43PnQAMMlC7mIZZDJoNVmJjRHCLmwxFJ88fm9qcV_v-rKiehIt_V_3L4c6BXxqUOwXVbI?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfSoWkIExAq9X-2fUkT8TsJVt2GLoh6VzN3f7dCV9PbAAnrxmYGmoFgo_w3nRa4W723WthfWi4tDANgSf-0Jts43PnQAMMlC7mIZZDJoNVmJjRHCLmwxFJ88fm9qcV_v-rKiehIt_V_3L4c6BXxqUOwXVbI?key=amEUHfTdJnvQeZF3EjeoeA)

Como vemos, es una contraseña muy segura.

Ahora, voy a descargarme una [extensión](https://chromewebstore.google.com/detail/administrador-de-contrase/pnlccmojcmeohlpggmfnbbiapkmbliob) de Chrome para administrar las contraseñas con RoboForm, para seguidamente registrarme en una página.

Para ello, es tan fácil como clickar en la opción de “Añadir a Chrome”:

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXcAbdPZPKCxiV9GsRFxNHT3hOQMdxdDYSwSSFuXJh85CToxzlhmVvQXQFDb5LvbIkrCmXTQGARfRcPe_khgVew_ffFZVtnAkq0nIOrcXLdX66r4MxH7Z-pDiSe0cRKkjDutazi-ZBey4UnXHugUlGYMB5Kh?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcAbdPZPKCxiV9GsRFxNHT3hOQMdxdDYSwSSFuXJh85CToxzlhmVvQXQFDb5LvbIkrCmXTQGARfRcPe_khgVew_ffFZVtnAkq0nIOrcXLdX66r4MxH7Z-pDiSe0cRKkjDutazi-ZBey4UnXHugUlGYMB5Kh?key=amEUHfTdJnvQeZF3EjeoeA)

Y añadimos la extensión:

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXd0YPD-y0TOhY7LdIp7C18gn-JzRB1DpPcxDy9s35HeylQk_5DRB9Eu6sMcL40CkDJRPWik8XwUJyVVexW-8OenRGheQrgIggqXvSHNFQPDAsHMrVjJP5Ib9-xA03wKu0jDSR5mmiPTw00hG7nrxLbY4338?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXd0YPD-y0TOhY7LdIp7C18gn-JzRB1DpPcxDy9s35HeylQk_5DRB9Eu6sMcL40CkDJRPWik8XwUJyVVexW-8OenRGheQrgIggqXvSHNFQPDAsHMrVjJP5Ib9-xA03wKu0jDSR5mmiPTw00hG7nrxLbY4338?key=amEUHfTdJnvQeZF3EjeoeA)

Nos pedirá crear una cuenta nueva:

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXcpYbbFFfR9tKoNb_u600DhmttG_JzMmC3QIr9XnDIrp_Kq2h0fE_RFMA_U-iUOhiS4sNOE2pyJQ6p3OobT5_4fLgZyPoas4zsmb0dTXEsjMDDQEpbALr0R6up86C4_bOt3kYC0aStxJXclLpSKKRparsIS?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcpYbbFFfR9tKoNb_u600DhmttG_JzMmC3QIr9XnDIrp_Kq2h0fE_RFMA_U-iUOhiS4sNOE2pyJQ6p3OobT5_4fLgZyPoas4zsmb0dTXEsjMDDQEpbALr0R6up86C4_bOt3kYC0aStxJXclLpSKKRparsIS?key=amEUHfTdJnvQeZF3EjeoeA)

Una vez añadido RoboForm, me registraré en HackTheBox y como se puede ver, a la hora de añadir la contraseña saldrá un icono de la aplicación:

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXcEg3Pqf8NxEqLUuKdXmtL_7QnOrW6vFkSLaggFPvSCXW_Z9lkFa82orrNUblI9Puxk_wm1OPXSlsnjfx4I-CPY84wQWKKvebhMgm3I3jrdodtREpk_fpygzIWWdxaZQGKLtIs_gYvTy6FeeaiJqBD0Pdg3?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcEg3Pqf8NxEqLUuKdXmtL_7QnOrW6vFkSLaggFPvSCXW_Z9lkFa82orrNUblI9Puxk_wm1OPXSlsnjfx4I-CPY84wQWKKvebhMgm3I3jrdodtREpk_fpygzIWWdxaZQGKLtIs_gYvTy6FeeaiJqBD0Pdg3?key=amEUHfTdJnvQeZF3EjeoeA)

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXfL7MV0gJz1yf4h4juNzjO9gWfLTPL0Dc_t1OlTl59Z2Ufs4q5hqa-QzjBMoidH7D9qnAI0DE5A6UiU5N2-WziSCl6oTA2xTjIbRAnrvjSmrQo49GITIa5B_rzeXZnB0NoNRaYMHBeti1EAqBC1eBQpCL0?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfL7MV0gJz1yf4h4juNzjO9gWfLTPL0Dc_t1OlTl59Z2Ufs4q5hqa-QzjBMoidH7D9qnAI0DE5A6UiU5N2-WziSCl6oTA2xTjIbRAnrvjSmrQo49GITIa5B_rzeXZnB0NoNRaYMHBeti1EAqBC1eBQpCL0?key=amEUHfTdJnvQeZF3EjeoeA)

La aplicación nos da la opción en vivo de generar una contraseña y rellenarla:

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXfaxac5zKq5RNKzP-0ndYtVZ-sBa1HQeSDNXgUQ7mB2ypl6lsgzJr5kUOcA7p1L0XFyK2AYgjJhA6xVdLAfWV6zbA0YcR9gLpcNj3ASuFbc7E9CXE5WnwROg0EwgFx8SA6k5tJNfpNfMyNZktnLxh0jVOjq?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfaxac5zKq5RNKzP-0ndYtVZ-sBa1HQeSDNXgUQ7mB2ypl6lsgzJr5kUOcA7p1L0XFyK2AYgjJhA6xVdLAfWV6zbA0YcR9gLpcNj3ASuFbc7E9CXE5WnwROg0EwgFx8SA6k5tJNfpNfMyNZktnLxh0jVOjq?key=amEUHfTdJnvQeZF3EjeoeA)

Y por supuesto nos la guardará en su almacenamiento para futuros inicios de sesión:

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXeOCr_JkPUPWDS7KK0pubVopUBo9D1TLqUV0ZGG6xybczHn3WCehQRI_e1R-5m5EEhTW3vn7NpLp9So71NDOG9_THIMQiHut6OAFhGUALWDCzIKe_BM4qn7CLFsYeHLsb0IRqj6oCYhk2H5qk5qUmWO5bLV?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeOCr_JkPUPWDS7KK0pubVopUBo9D1TLqUV0ZGG6xybczHn3WCehQRI_e1R-5m5EEhTW3vn7NpLp9So71NDOG9_THIMQiHut6OAFhGUALWDCzIKe_BM4qn7CLFsYeHLsb0IRqj6oCYhk2H5qk5qUmWO5bLV?key=amEUHfTdJnvQeZF3EjeoeA)

Ya estaríamos registrados con una contraseña segura:

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXfVXltbaSxvD9QBgHjJCN_Msjg6ImUC8cr89ANXJW4u8lGi1CU7eoTKAGIv2zWAYgdlbYUlu0Kj-ac6nOBRrT5i8Wot1_T_xVWASjA3tNxUaMNQPfg34TKvtZy_EMHgLUx8dhko06lmQiiQoCYu_fYAhUZA?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfVXltbaSxvD9QBgHjJCN_Msjg6ImUC8cr89ANXJW4u8lGi1CU7eoTKAGIv2zWAYgdlbYUlu0Kj-ac6nOBRrT5i8Wot1_T_xVWASjA3tNxUaMNQPfg34TKvtZy_EMHgLUx8dhko06lmQiiQoCYu_fYAhUZA?key=amEUHfTdJnvQeZF3EjeoeA)

### **Herramientas del sistema**

En un sistema como Debian 12, es fundamental asegurar que las contraseñas utilizadas por los usuarios sean fuertes y seguras para proteger el sistema contra posibles ataques.

Por ejemplo, existen herramientas que vienen por defecto en el sistema como **PAM** (Pluggable Authentication Modules). PAM es un marco de autenticación que permite a los administradores de sistemas configurar políticas de autenticación flexibles. En Debian 12, se pueden configurar reglas para la complejidad de las contraseñas utilizando el módulo *pam_pwquality*. Para instalarlo:

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXfwZE21v_aTl3E8I8Nf8eMgjU3LsGg6YjfRzJAX6zu-65U7y_I0SPlB0hnz8uEci3XQ0sHxnYoUTfW7xiwbbUwpWRQOn23bvu_VPVJ7UrguD6fkzc8bsT2LCcPEHlovRzI1Rp0RRoSIK9RorGJ27tZLcoqR?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfwZE21v_aTl3E8I8Nf8eMgjU3LsGg6YjfRzJAX6zu-65U7y_I0SPlB0hnz8uEci3XQ0sHxnYoUTfW7xiwbbUwpWRQOn23bvu_VPVJ7UrguD6fkzc8bsT2LCcPEHlovRzI1Rp0RRoSIK9RorGJ27tZLcoqR?key=amEUHfTdJnvQeZF3EjeoeA)

Para hacerlo es tan sencillo como dirigirnos al archivo de configuración:

```powershell
*sudo nano /etc/pam.d/common-password*
```

En la línea que contiene *pam_pwquality.so* añadimos cualquier parámetro para establecer requisitos de seguridad, como la longitud mínima de la contraseña o la mezcla de caracteres:

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXdKtK6NE5cU_kjMP9pv0ljC2j51YHf8PMGK42eNkoH5GlmBPVfLJs3tr0Y_Er8r3PsL3uBy0iQuZpSQjBk-9IR1m33UTYoscM1d9yu3Lx9ciU5CKOoRJ2OqWAGgcrOzmtuHZyEKWMiXMKqV3ciLMRtkPph8?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdKtK6NE5cU_kjMP9pv0ljC2j51YHf8PMGK42eNkoH5GlmBPVfLJs3tr0Y_Er8r3PsL3uBy0iQuZpSQjBk-9IR1m33UTYoscM1d9yu3Lx9ciU5CKOoRJ2OqWAGgcrOzmtuHZyEKWMiXMKqV3ciLMRtkPph8?key=amEUHfTdJnvQeZF3EjeoeA)

- **retry=3**: Permite tres intentos de establecer una contraseña que cumpla con las reglas antes de bloquear el intento de cambio de contraseña.
- **minlen=12**: Establece una longitud mínima de 12 caracteres para la contraseña.
- **ucredit=-1**: Requiere al menos una letra mayúscula.
- **lcredit=-1**: Requiere al menos una letra minúscula.
- **dcredit=-1**: Requiere al menos un dígito.
- **ocredit=-1**: Requiere al menos un carácter especial (como !@#$%).

Reiniciamos:

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXf688jQNgWUxBLHbIB4VgYtPg9VtZyLF7mKmWYQMceUEZCdswWOxAlnF7YG_dsYyCKYpL1o_3xAJcv6Gz8VLMgkGiEkRrs7ZqcVyu0dQI6UQycSrwc6YUhrvmyazqIY1pQiEjjDkpGpiZgMot81QpyotdX0?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf688jQNgWUxBLHbIB4VgYtPg9VtZyLF7mKmWYQMceUEZCdswWOxAlnF7YG_dsYyCKYpL1o_3xAJcv6Gz8VLMgkGiEkRrs7ZqcVyu0dQI6UQycSrwc6YUhrvmyazqIY1pQiEjjDkpGpiZgMot81QpyotdX0?key=amEUHfTdJnvQeZF3EjeoeA)

Y una vez añadido estos parámetros podemos hacer una comprobación cambiando la contraseña de mi usuario, por ejemplo:

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXeesc4zJge44F0-VaqQxICxBAMFiZ0aTCGiAtTxGdwXnuCkGhwydPIUqI5RBAR5ZuUEPV44noKdiFbUk6DxlNixcPT5Z_ETbJjDKgJnV_AHa4i0Kt-bHg-VlnZTUS2wRFSOkVxZg2eN3_0AzI806xFqTTBu?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeesc4zJge44F0-VaqQxICxBAMFiZ0aTCGiAtTxGdwXnuCkGhwydPIUqI5RBAR5ZuUEPV44noKdiFbUk6DxlNixcPT5Z_ETbJjDKgJnV_AHa4i0Kt-bHg-VlnZTUS2wRFSOkVxZg2eN3_0AzI806xFqTTBu?key=amEUHfTdJnvQeZF3EjeoeA)

En este ejemplo vemos que si la contraseña no tiene dígitos, no tiene mayúsculas o de alguna forma se lee el nombre de usuario, nos dará error.

## **John The Ripper**

### **¿Qué es John the Ripper?**

John the Ripper es una **herramienta en C** ampliamente utilizada en ciberseguridad para verificar la fortaleza de contraseñas, probando su resistencia a ataques de fuerza bruta. Es capaz de descifrar varios tipos de hashes comunes como **MD5 y SHA-1** sin que el usuario deba preocuparse por identificarlos previamente, ya que el programa los detecta automáticamente. Esto hace que su uso sea más accesible para los analistas de seguridad.

Esta herramienta, optimizada para múltiples arquitecturas de procesadores y sistemas operativos, es especialmente popular en Linux y se incluye por defecto en distribuciones de pentesting. Además, es altamente configurable: permite ajustar la longitud de las contraseñas a probar, definir rangos de letras, números y símbolos, y establecer reglas específicas para variar las combinaciones.

Una de las ventajas de John the Ripper es la posibilidad de pausar el proceso de crackeo y continuarlo más tarde. Incluso se puede configurar para comenzar automáticamente al iniciar el equipo, lo que lo hace flexible y adaptable al entorno del usuario.

En administración de sistemas, John the Ripper se usa para asegurarse de que las contraseñas de los usuarios sean seguras, sin que sea necesario conocerlas, y la versión gratuita es suficiente para estas evaluaciones de seguridad básicas.

### **Funcionamiento**

El proceso de crackeo de contraseñas con John the Ripper consiste en:

1. Generar hashes de contraseñas potenciales
2. Comparar estos hashes con el hash objetivo que se intenta crackear
3. Si hay coincidencia, se ha encontrado la contraseña

### **Modos de operación**

John the Ripper ofrece varios modos de funcionamiento:

1. **Modo single**: Usa la información del archivo /etc/passwd para crear un diccionario específico y atacar una cuenta particular.
2. **Modo por diccionario**: Utiliza un diccionario externo y permite aplicar reglas (--rules) y máscaras (--mask) para generar variaciones en las palabras del diccionario, combinando patrones y diccionario.
3. **Modo de fuerza bruta/incremental**: Genera todas las combinaciones posibles de caracteres basándose en configuraciones predeterminadas en john.conf. También permite usar máscaras para limitar los patrones generados.
4. **Modo externo**: Permite definir ataques personalizados a través de código en john.conf, ofreciendo flexibilidad para crear estrategias avanzadas de ataque.

### **Instalación y uso**

Para realizar la instalación en Debian 12 existen varias formas, una de ellas es hacerlo con snap. Este es un sistema de gestión de paquetes universales e implementación de software diseñado y creado por Canonical. Para ello instalamos la herramienta snapd y luego lo instalamos:  

```powershell
*sudo apt-get install snapd* 
```

```powershell
*sudo snap install john-the-ripper*
```

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXfnfSxC-2kkNuaxzSOzupH5hAPJro1eBzKXZB4Ur39TTrFxrBB1dXSI8a3OZyeO2vhARLJra2IFPLsbDojrUZuEd5EraDCKgUmsK_EPsN08rD67yMXOV_Ucsh3zqMyeoCwRnaPW1tHL05BCyvMETfmIpFc?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfnfSxC-2kkNuaxzSOzupH5hAPJro1eBzKXZB4Ur39TTrFxrBB1dXSI8a3OZyeO2vhARLJra2IFPLsbDojrUZuEd5EraDCKgUmsK_EPsN08rD67yMXOV_Ucsh3zqMyeoCwRnaPW1tHL05BCyvMETfmIpFc?key=amEUHfTdJnvQeZF3EjeoeA)

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXdcsJ7aikuhvD5uoWe8wnn5sfB0jxOp9RjQ7QC97iE9M2vMG4pD3FvIy5LZ9MNqJPLPV4JFmYYy5vjqUQJWyTduzmxPEQoaUgNnmvy-3f9c9jlVmmfhTx0_lTCuP-kUnyr-ekyaMJ5HhbHgr0FncRPAv5Y?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdcsJ7aikuhvD5uoWe8wnn5sfB0jxOp9RjQ7QC97iE9M2vMG4pD3FvIy5LZ9MNqJPLPV4JFmYYy5vjqUQJWyTduzmxPEQoaUgNnmvy-3f9c9jlVmmfhTx0_lTCuP-kUnyr-ekyaMJ5HhbHgr0FncRPAv5Y?key=amEUHfTdJnvQeZF3EjeoeA)

La otra opción es hacerlo directamente con la paquetería de repositorios oficiales de Debian:

```powershell
sudo apt install john
```

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXdbBRcfJy-7tPoB57F-vsewDYSMK2bjdWbvFEFudJlurtxVzi9jmFszgrgQsEIphmKyax57ahvBkKtshtjdCA1acQ5zDaMQKpzvu6L9RRWJwjTymVUK6suRo8Ohpcw3qs4xK48287KUEeQ6gkvq4pmzleOB?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdbBRcfJy-7tPoB57F-vsewDYSMK2bjdWbvFEFudJlurtxVzi9jmFszgrgQsEIphmKyax57ahvBkKtshtjdCA1acQ5zDaMQKpzvu6L9RRWJwjTymVUK6suRo8Ohpcw3qs4xK48287KUEeQ6gkvq4pmzleOB?key=amEUHfTdJnvQeZF3EjeoeA)

Antes de iniciar el crackeo de contraseñas, podemos ejecutar una prueba de rendimiento sencilla que pondrá a prueba nuestro hardware. Esto nos permitirá conocer la velocidad con la que John the Ripper probará contraseñas en diferentes tipos de cifrado, utilizando al máximo la CPU. Para hacer esto, basta con abrir una terminal en Linux y escribir:

```powershell
sudo john --test
```

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXebJ40GP9t_-kpd86v7qPRFpqkP5OraM-hC8XohO0OqBlsJMjVraqtlhqQV4CaPmTsojZFubayIt0-mvDhMoWre3E3WVJD7p0D0cagZkgzLAWibEsJUcxVdLv9pWQKHT75Tq77ILXGaBNYIBSGLj4kWC3Q?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXebJ40GP9t_-kpd86v7qPRFpqkP5OraM-hC8XohO0OqBlsJMjVraqtlhqQV4CaPmTsojZFubayIt0-mvDhMoWre3E3WVJD7p0D0cagZkgzLAWibEsJUcxVdLv9pWQKHT75Tq77ILXGaBNYIBSGLj4kWC3Q?key=amEUHfTdJnvQeZF3EjeoeA)

Como vemos, se realizan una serie de mediciones de rendimiento para evaluar la capacidad de procesamiento de nuestro equipo.

### **Crackeo de contraseñas por fuerza bruta**

Un ataque de fuerza bruta con John the Ripper implica probar todas las combinaciones posibles de caracteres hasta encontrar una coincidencia con el hash de la contraseña objetivo. Este tipo de ataque es el más exhaustivo, y se utiliza cuando no se dispone de un diccionario de contraseñas o cuando se desea romper una contraseña especialmente compleja.

Podría optar por usar el fichero /etc/shadow directamente, que es el archivo que contiene las contraseñas de Linux. Pero en este caso voy a crear manualmente un fichero con distintos usuarios y contraseñas para hacer la prueba. Pues de esta forma se realizará de forma más rápida y además, no comprometemos nuestro sistema.

Bien, en primer lugar tendremos que elegir las contraseñas para los usuarios y luego generar los hashes:

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXfsc5CWOGbM23JIO089rWcjTwrUVpfBeIFbrJ1r4Z2DGJSZWr3sAq1U0T9WGTF7_7_DwrSYCkh3tAi2GL7PWpT_z3Hvf4o6JMYBAjB6p4OVtohWPmDpuRLWbN2l3jF-z2J5X1r8TuxnXVoQWn0Sv9nDgyTR?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfsc5CWOGbM23JIO089rWcjTwrUVpfBeIFbrJ1r4Z2DGJSZWr3sAq1U0T9WGTF7_7_DwrSYCkh3tAi2GL7PWpT_z3Hvf4o6JMYBAjB6p4OVtohWPmDpuRLWbN2l3jF-z2J5X1r8TuxnXVoQWn0Sv9nDgyTR?key=amEUHfTdJnvQeZF3EjeoeA)

- **openssl passwd -1 password** genera un hash de contraseña con el algoritmo MD5.
- **>> password.txt** guarda cada línea (usuario y hash) en el archivo **password.txt**.

Verificamos el archivo password.txt, debería verse así:

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXdHh6AeLnaTvEqndlSMAYqE_kHlmkORKj7wFwPkb33lgvTxuAo4Y9PTDPihaw-tDOGnWdejb2LAp1eOD8nFZ-82dLVYgNL2M0ge6739MgN6HZFGwQtGcmJmOldwuJ3bg1q0Y3pQiHzn61Q8BAyoddRn6ICv?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdHh6AeLnaTvEqndlSMAYqE_kHlmkORKj7wFwPkb33lgvTxuAo4Y9PTDPihaw-tDOGnWdejb2LAp1eOD8nFZ-82dLVYgNL2M0ge6739MgN6HZFGwQtGcmJmOldwuJ3bg1q0Y3pQiHzn61Q8BAyoddRn6ICv?key=amEUHfTdJnvQeZF3EjeoeA)

A continuación, vamos a indicar a John que empiece a trabajar para crackear la contraseña del archivo anterior:

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXd_ELCGpFzGX3DIUWYh7opj8Viq_QL_c7q1t8skCeOZtsAVFwFWs5tIBuHAnNuv2Nt8O-qQhyzIM-R3-IF0K7ygpL-mtVAxfcw9smND4My8ErYi2_0onRcVIiTbQN4H-HoD5RfrELbb7OKf7ttbyPf84j3X?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXd_ELCGpFzGX3DIUWYh7opj8Viq_QL_c7q1t8skCeOZtsAVFwFWs5tIBuHAnNuv2Nt8O-qQhyzIM-R3-IF0K7ygpL-mtVAxfcw9smND4My8ErYi2_0onRcVIiTbQN4H-HoD5RfrELbb7OKf7ttbyPf84j3X?key=amEUHfTdJnvQeZF3EjeoeA)

Mientras John the Ripper trabaja, mostrará el progreso en la terminal. Puede llevar algo de tiempo, dependiendo de la complejidad de las contraseñas. En este caso ha tardado muy poco, pues son contraseñas sencillas.

Una vez que finalice el proceso, podemos ver las contraseñas crackeadas:

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXcB7lr1S99oMWPjMU4QyX4EI9QWDOGQJRk8shQUkXi0IAmnIoiAtqXpwrorLB6wC0Am-IzzvGLK3G6YFqJxERCmcHXqlWkLUhzPlGDSLkkOXpQqMhTPOF3eYJ3jrBClIQaEb__Y0ua-Rd19rNq7fc_2X-E?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcB7lr1S99oMWPjMU4QyX4EI9QWDOGQJRk8shQUkXi0IAmnIoiAtqXpwrorLB6wC0Am-IzzvGLK3G6YFqJxERCmcHXqlWkLUhzPlGDSLkkOXpQqMhTPOF3eYJ3jrBClIQaEb__Y0ua-Rd19rNq7fc_2X-E?key=amEUHfTdJnvQeZF3EjeoeA)

Otra forma para generar los hashes de las contraseñas de manera sencilla es usando mkpasswd con el método SHA-512. mkpasswd es una herramienta que pertenece al paquete whois en Debian, por lo que debemos instalarlo primero:

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXdQDx9ZvPVioWXRNF_C-4WOP2ukolu3m2GlNeDN1xb6rIrCYRV9rdCr2w2Tbd0ZQ11x9A3eUtbWAm1VoxC00qTRYR-G-24Mkkv0WpkwzKJ5QAmYzUUqQyL1kqA2lyImdTBcutObW5GVPeaSUk4PaqhlUFM6?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdQDx9ZvPVioWXRNF_C-4WOP2ukolu3m2GlNeDN1xb6rIrCYRV9rdCr2w2Tbd0ZQ11x9A3eUtbWAm1VoxC00qTRYR-G-24Mkkv0WpkwzKJ5QAmYzUUqQyL1kqA2lyImdTBcutObW5GVPeaSUk4PaqhlUFM6?key=amEUHfTdJnvQeZF3EjeoeA)

Ahora, generamos una contraseña con la nueva funcionalidad:

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXeNxQ9yY-CfO-Ka5hugX0ohkMAiCNaAGe4LZgWWXF2fs0HQ7sGUocrrbsURKDSR4Hda7niROtG3rgV9pHqJTJSg0mLSnG8yvLUL4YRyYnlcrkRX3ImUDJNzmJIX-c9DS8subkm4OzR7hv6JQg0b0V8gsoWh?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeNxQ9yY-CfO-Ka5hugX0ohkMAiCNaAGe4LZgWWXF2fs0HQ7sGUocrrbsURKDSR4Hda7niROtG3rgV9pHqJTJSg0mLSnG8yvLUL4YRyYnlcrkRX3ImUDJNzmJIX-c9DS8subkm4OzR7hv6JQg0b0V8gsoWh?key=amEUHfTdJnvQeZF3EjeoeA)

Verificamos el contenido del archivo:

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXcUZiTeEmvTOA0_PnxROBOqDqx5k4Gf3kkX-iGdgzN5Cl_nLObFC6RCY3wGxsJZ3rSZd2z5_d5_ROY8QPwiU71A9Pnf22BFZP5vVoEtykGwiTUSuG8GwN-ZfFrKk1maxKWnaS8wYWpzFXD9J5PQDe5By2Ie?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcUZiTeEmvTOA0_PnxROBOqDqx5k4Gf3kkX-iGdgzN5Cl_nLObFC6RCY3wGxsJZ3rSZd2z5_d5_ROY8QPwiU71A9Pnf22BFZP5vVoEtykGwiTUSuG8GwN-ZfFrKk1maxKWnaS8wYWpzFXD9J5PQDe5By2Ie?key=amEUHfTdJnvQeZF3EjeoeA)

Y crackeamos la contraseña:

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXf4jUxG_5cUa1ygjYGRwbAg8OgSdC36IHBZv-8xJ3pWrqG2vLcNZhpqRv9yIPju2fz1hWjUf-gaOzry1Rd3-dgwK-nwhvSlGW6cIL6LoEpoCPgTalSlYOzPb5d6PGrZb4Ro0y0td5EC4rBzoI1aIUt6DJUZ?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf4jUxG_5cUa1ygjYGRwbAg8OgSdC36IHBZv-8xJ3pWrqG2vLcNZhpqRv9yIPju2fz1hWjUf-gaOzry1Rd3-dgwK-nwhvSlGW6cIL6LoEpoCPgTalSlYOzPb5d6PGrZb4Ro0y0td5EC4rBzoI1aIUt6DJUZ?key=amEUHfTdJnvQeZF3EjeoeA)

Como vemos, John ha encontrado la contraseña "messi" para el usuario "pablomartin" en 7 minutos y 43 segundos.

Para mostrar la contraseña descifrada:

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXeDfp-XNzaF6kKXgmCRtbM5pPmaQY5_vdI1wd-4P7dt6Zg6FlpCAxnF8kw_HBWQfFXhDMAAQ6yPzYzwzQtnvvF8q2xKJqaHTNlIeB6-295-DB1ZAnFViaqeZmLG78b4cCG4757zSBZiSrZiKXAoSD73AwE?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeDfp-XNzaF6kKXgmCRtbM5pPmaQY5_vdI1wd-4P7dt6Zg6FlpCAxnF8kw_HBWQfFXhDMAAQ6yPzYzwzQtnvvF8q2xKJqaHTNlIeB6-295-DB1ZAnFViaqeZmLG78b4cCG4757zSBZiSrZiKXAoSD73AwE?key=amEUHfTdJnvQeZF3EjeoeA)

### **Crackeo de Contraseñas Usando un Diccionario**

El crackeo de contraseñas utilizando un diccionario es un enfoque que utiliza una lista de posibles contraseñas para intentar adivinar la contraseña real. Este método es efectivo para contraseñas comunes o débiles que están presentes en el diccionario.

**Diccionario por Defecto en John the Ripper**

Por defecto, John the Ripper incluye un diccionario llamado password.lst, que se encuentra en la ruta:

```powershell
/usr/share/john/password.lst
```

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXexQfqGY0m3j-76FfvKH4Gh_kx8mNebrY4sjTxnzldoPRTt5EsvAcK6AYGcEljaNXVwlfXBaM70GitX0T9_FWqL00fR1uCYimVuMuyhzzfxZWJQ1N5mCq-1CJlLQ3jdGRosrQwFgz9SsKhpOFO2HLYWk8aB?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXexQfqGY0m3j-76FfvKH4Gh_kx8mNebrY4sjTxnzldoPRTt5EsvAcK6AYGcEljaNXVwlfXBaM70GitX0T9_FWqL00fR1uCYimVuMuyhzzfxZWJQ1N5mCq-1CJlLQ3jdGRosrQwFgz9SsKhpOFO2HLYWk8aB?key=amEUHfTdJnvQeZF3EjeoeA)

Este archivo contiene una lista de contraseñas comunes y se utiliza durante el proceso de crackeo. John intentará todas las contraseñas en este diccionario para encontrar coincidencias con los hashes que se proporcionen.

**Descargar el Diccionario rockyou.txt**

Uno de los diccionarios más conocidos y utilizados para crackear contraseñas es rockyou.txt. Este archivo fue creado a partir de una brecha de seguridad en el sitio web RockYou en 2009 y contiene millones de contraseñas reales. Para descargarlo lo he hecho a través de este repositorio de GitHub →[https://github.com/brannondorsey/naive-hashcat/releases/download/data/rockyou.txt](https://github.com/brannondorsey/naive-hashcat/releases/download/data/rockyou.txt)

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXfs-jtK8ZZGRTLGHY5T-4bBfr9vhRItMNBgwNVNgMyTqap8QuhE6NQtvSpNOVuDdPIGckda7Aa72-k7zMLPQ8P2pqjvi0wChv3KPUiCychNsCy8ObOqkw45gwMDsKXb32FiXiLC62tjV2HDBIrKXtBEqc0?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfs-jtK8ZZGRTLGHY5T-4bBfr9vhRItMNBgwNVNgMyTqap8QuhE6NQtvSpNOVuDdPIGckda7Aa72-k7zMLPQ8P2pqjvi0wChv3KPUiCychNsCy8ObOqkw45gwMDsKXb32FiXiLC62tjV2HDBIrKXtBEqc0?key=amEUHfTdJnvQeZF3EjeoeA)

Ahora lo combinaré con el diccionario password.lst para tener un único diccionario:

```powershell
cat rockyou.txt >> password.lst
```

Por ejemplo, si hacemos una búsqueda de la contraseña “prueba” nos devolverá todas las contraseñas filtradas que contengan la palabra:

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXcQf8WfbKeqjxNyOoDz_q6sEbGhP2KtNoASPLYXe7oE_XOb_9QkRNUmVhDVF2yP1b1Na3DXkSv9stDo4UOXHN7y1vdHwCh8uZGDLduNR9VNzQ2lWW1QlTku443JwpFe0ZyACXvXohMjBS43U3kKW1zW-Cei?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcQf8WfbKeqjxNyOoDz_q6sEbGhP2KtNoASPLYXe7oE_XOb_9QkRNUmVhDVF2yP1b1Na3DXkSv9stDo4UOXHN7y1vdHwCh8uZGDLduNR9VNzQ2lWW1QlTku443JwpFe0ZyACXvXohMjBS43U3kKW1zW-Cei?key=amEUHfTdJnvQeZF3EjeoeA)

Ahora voy a crear 5 usuarios en el sistema y sus contraseñas. Para fines de demostración, utilizaré contraseñas simples. Los usuarios se crearán con comandos que se agregarán a los archivos **/etc/shadow** y **/etc/passwd**.

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXdhwjATFnNr_Hsb-tA3XwKaFUlMpnHbkgbhZgZvTbxgBV2oQnN7KJazYpEQ1tg1XPlqii-U-ijOYLht9DoBm8IZKgrvws4kkKbfn4UXFS5NxoPrVT5yriwsxzaLFWgFQ-bAgolLx2ijZgOjbaqzoKO7J2cO?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdhwjATFnNr_Hsb-tA3XwKaFUlMpnHbkgbhZgZvTbxgBV2oQnN7KJazYpEQ1tg1XPlqii-U-ijOYLht9DoBm8IZKgrvws4kkKbfn4UXFS5NxoPrVT5yriwsxzaLFWgFQ-bAgolLx2ijZgOjbaqzoKO7J2cO?key=amEUHfTdJnvQeZF3EjeoeA)

Podemos verificar que los usuarios han sido creados correctamente revisando los archivos **/etc/passwd** y **/etc/shadow**:

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXeMolkkWTkpU1fSLoJUYg0xRMu-Zgnx_h4Myl1BrUtnJCPzKHgci4O8Wxnr4vHg2SIAXeRul5b-eMPTEFv8Q0gzk9fUOS6G4ZhNCEVk5wbWv53XCk2NqVdXVop8gkpzf-z6U_RRlXz29SobdK9jZObQnZLU?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeMolkkWTkpU1fSLoJUYg0xRMu-Zgnx_h4Myl1BrUtnJCPzKHgci4O8Wxnr4vHg2SIAXeRul5b-eMPTEFv8Q0gzk9fUOS6G4ZhNCEVk5wbWv53XCk2NqVdXVop8gkpzf-z6U_RRlXz29SobdK9jZObQnZLU?key=amEUHfTdJnvQeZF3EjeoeA)

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXeT-wluS_6SREud_bSAqDXuTzF-6ILRL6LDIcvDPrWg6dlz2jrqNJ_C8b9Vk5z2Ebjf8LE3-SOUmJpMdbGtazQ-enrQqOzHxBRA9No_i1o33auSGk3Dje2dMcs6CG0Yg47Lw9ZRb5lhIq5M44BoJLq98S_Y?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeT-wluS_6SREud_bSAqDXuTzF-6ILRL6LDIcvDPrWg6dlz2jrqNJ_C8b9Vk5z2Ebjf8LE3-SOUmJpMdbGtazQ-enrQqOzHxBRA9No_i1o33auSGk3Dje2dMcs6CG0Yg47Lw9ZRb5lhIq5M44BoJLq98S_Y?key=amEUHfTdJnvQeZF3EjeoeA)

**Preparar los Archivos de Usuarios y Contraseñas**

El archivo **/etc/passwd** contiene información sobre todos los usuarios del sistema, incluyendo el nombre de usuario y la información de la cuenta. Para este ejemplo, extraemos las últimas cinco líneas, que representan a los últimos cinco usuarios añadidos en el sistema.

```powershell
tail -n 5 /etc/passwd > passwd.txt
```

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXcA_r4KO4EyfCo7Axo8VSVWj1K1w_6qvQEuoItDuAsH0NexsLt3LoZItzG4NNUQVs0h63PZNSkgR7avium2odj1-Kl0qI4GLfA1qf61I_Ry7zM9tg9ShqVElz4DSV5pH03f4fX05QPlEp7b6XcnYChKJbOI?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcA_r4KO4EyfCo7Axo8VSVWj1K1w_6qvQEuoItDuAsH0NexsLt3LoZItzG4NNUQVs0h63PZNSkgR7avium2odj1-Kl0qI4GLfA1qf61I_Ry7zM9tg9ShqVElz4DSV5pH03f4fX05QPlEp7b6XcnYChKJbOI?key=amEUHfTdJnvQeZF3EjeoeA)

El archivo **/etc/shadow** contiene los hashes de las contraseñas de los usuarios, que son necesarios para el proceso de crackeo. Usamos el mismo enfoque para extraer las últimas cinco líneas:

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXdOznnaBo3jxdXCSlChkvoHGuvDySYoZNbT1e1wElCuuWJyJefdbsywrbREdOpLaXrIhTRa7GV_EMR8_-jny-W-2oehDK2tlic6h9AqGK5uydgS5A_kWmllqec9ENZvkWHEdGl2hWK0a7v-_KgCS6xKZWs?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdOznnaBo3jxdXCSlChkvoHGuvDySYoZNbT1e1wElCuuWJyJefdbsywrbREdOpLaXrIhTRa7GV_EMR8_-jny-W-2oehDK2tlic6h9AqGK5uydgS5A_kWmllqec9ENZvkWHEdGl2hWK0a7v-_KgCS6xKZWs?key=amEUHfTdJnvQeZF3EjeoeA)

John the Ripper necesita un formato específico que combine los datos de ambos archivos. Utilizamos la herramienta **unshadow** para crear un archivo que contenga los nombres de usuario junto con sus hashes de contraseñas:

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXfcgpovl_dHOWxNIl8aTITrxWKhAWOzkpw5V9tiFgKh8Ve8IqQluJz66OtmMX40iiQtRsjY4FSLfgInbfrRhU5q2TH-ExQRP0ZRcTmaQthFL2W8rEulKIggqwElH_qqmBZ6-6vgEe0PjtewN17NR_0KxNYd?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfcgpovl_dHOWxNIl8aTITrxWKhAWOzkpw5V9tiFgKh8Ve8IqQluJz66OtmMX40iiQtRsjY4FSLfgInbfrRhU5q2TH-ExQRP0ZRcTmaQthFL2W8rEulKIggqwElH_qqmBZ6-6vgEe0PjtewN17NR_0KxNYd?key=amEUHfTdJnvQeZF3EjeoeA)

**Crackeo**

Ahora que tenemos el archivo de contraseñas preparado, podemos ejecutar John the Ripper para iniciar el proceso de crackeo. Utilizamos un diccionario de contraseñas que John utilizará para intentar adivinar las contraseñas:

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXfVh6AtXewVPAo31nJNlPE1HmTJVsQd8UUuqPIf1iX-HA5_CUDM_18R5l7jT-se5xV649p9D23-wTW3W3Q1DNmobwq3rOZtiNM3vUBwxytVnyBfbNF9OHwaluAWG3gHjnaDTDHTNhHZOeLt37r3ZpkA2cAZ?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfVh6AtXewVPAo31nJNlPE1HmTJVsQd8UUuqPIf1iX-HA5_CUDM_18R5l7jT-se5xV649p9D23-wTW3W3Q1DNmobwq3rOZtiNM3vUBwxytVnyBfbNF9OHwaluAWG3gHjnaDTDHTNhHZOeLt37r3ZpkA2cAZ?key=amEUHfTdJnvQeZF3EjeoeA)

Una vez completado, podemos usar el siguiente comando para ver las contraseñas que se han crackeado:

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXcwzulwqrc0eKYkTM0Zdnmn2aQkFMnEcjSnYcJuVjlKiRLB2uiBvUwxKN1tnmROV8ugpTbkryr3JHpQ7shdMJgLMzcqcToHm06gdl7hccpbumzXZ1tM1odOnPt-NI9y8BfYxYickH7JD2rHp9Z9uCm3N-4?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcwzulwqrc0eKYkTM0Zdnmn2aQkFMnEcjSnYcJuVjlKiRLB2uiBvUwxKN1tnmROV8ugpTbkryr3JHpQ7shdMJgLMzcqcToHm06gdl7hccpbumzXZ1tM1odOnPt-NI9y8BfYxYickH7JD2rHp9Z9uCm3N-4?key=amEUHfTdJnvQeZF3EjeoeA)

### **Modificación de reglas en diccionarios**

Las reglas de modificación permiten a John the Ripper alterar las palabras del diccionario para generar más candidatos de contraseña. Esto es útil porque muchos usuarios modifican palabras comunes para crear sus contraseñas.

Voy a crear un conjunto de reglas más complejo que combine varias transformaciones:

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXep8VSu1UZnl944p-LVnP1ZtUuR0pawMcdvZxswTfDYnSj-36nGCnZ04yYFKdsccMo4NigFeQj5GA9sehvhOBZWRZMV7OObTe_fsT-s0XVMhZvlHXlxlDQT0_azb2mg595RrMrSUeGnITLMTm40ldgabhTf?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXep8VSu1UZnl944p-LVnP1ZtUuR0pawMcdvZxswTfDYnSj-36nGCnZ04yYFKdsccMo4NigFeQj5GA9sehvhOBZWRZMV7OObTe_fsT-s0XVMhZvlHXlxlDQT0_azb2mg595RrMrSUeGnITLMTm40ldgabhTf?key=amEUHfTdJnvQeZF3EjeoeA)

He añadido la sección “ComplexRules”.

Este conjunto de reglas hará lo siguiente:

- Capitaliza la primera letra y añadirá dos dígitos al final
- Sustituirá 'a' por '@' y 'o' por '0'
- Invertirá la palabra y añadirá un carácter especial al final

Por ejemplo, la palabra "password" se transformará en:

- Password00, Password01, ..., Password99
- p@$$w0rd
- drowssap!, drowssap@, drowssap#, ...

Este enfoque aumenta significativamente las posibilidades de crackear contraseñas más complejas que son variaciones de palabras comunes.

Para aplicar las nuevas reglas ejecutamos el siguiente comando:

```powershell
john --stdout --wordlist=password.lst --rules
```

Ahora, redigiré el diccionario con las nuevas reglas a un diccionario vacío

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXfVcN_39yQFJ3De9GQnvfu3J1AvnBJS6gAraUosnd1pihmVse9lcPtXs0aZGU0_tyntkqQWher8D29TjtLgFEIw8VHK_lq4ciNRsKshJTJlnkSIGZeViDhH7qjifIY920EPie60AOq_51tsKDz7hbUqzyU?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfVcN_39yQFJ3De9GQnvfu3J1AvnBJS6gAraUosnd1pihmVse9lcPtXs0aZGU0_tyntkqQWher8D29TjtLgFEIw8VHK_lq4ciNRsKshJTJlnkSIGZeViDhH7qjifIY920EPie60AOq_51tsKDz7hbUqzyU?key=amEUHfTdJnvQeZF3EjeoeA)

Creamos un usuario con contraseña para el test:

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXfT4eaHl1J2T_lYaKPwFV9WItJ1rUzAi2kwsRbHj1g7sO8vrIkiafC2uf1r3DVpkPNYG4G0wSUZhHLSBrn5BgN21q3Ufgyo5JB0iOTTgn8hpx3ng4OubkXLiTgl_0N1nEGGggkPw0jEkscDlOskLH-Hdg0v?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfT4eaHl1J2T_lYaKPwFV9WItJ1rUzAi2kwsRbHj1g7sO8vrIkiafC2uf1r3DVpkPNYG4G0wSUZhHLSBrn5BgN21q3Ufgyo5JB0iOTTgn8hpx3ng4OubkXLiTgl_0N1nEGGggkPw0jEkscDlOskLH-Hdg0v?key=amEUHfTdJnvQeZF3EjeoeA)

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXftizZ31XxJHzWg9k6ha3CSWfWIT4kzYsTPCvdduoNxJzS5QoWfj7GH0n-wrgoS7e8_ici-4AY4tQhkOo5sFarMKjyx4zw6wa4ub8K7L-hqQYoNFTT1Zi27nI_3HkPvfWfSs_9gyNLSLZtxFOL0gxn9AHfx?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXftizZ31XxJHzWg9k6ha3CSWfWIT4kzYsTPCvdduoNxJzS5QoWfj7GH0n-wrgoS7e8_ici-4AY4tQhkOo5sFarMKjyx4zw6wa4ub8K7L-hqQYoNFTT1Zi27nI_3HkPvfWfSs_9gyNLSLZtxFOL0gxn9AHfx?key=amEUHfTdJnvQeZF3EjeoeA)

Por último, crackeamos la contraseña con el parámetro –rules para que se apliquen las modificaciones. Tras más de un día, la búsqueda de la contraseña ha seguido, por lo que no puedo demostrar que se ha crackeado, pero el funcionamiento es el correcto.

# Responsabilidad grupal

## 1. Documentad la aplicación de las distintas herramientas a un escenario en el que tenemos una máquina con un servicio Nginx y otro Postgres que son accedidos por una máquina cliente Windows y otra Linux. Debéis crear los usuarios que consideréis necesarios. En dicha documentación debe incluirse también las conclusiones sobre la utilidad de cada herramienta y en qué contexto ven necesaria su utilización.

## 2. Reconocimiento pasivo y activo

## Reconocimiento pasivo

### **1. Usad el comando whois para averiguar información de un dominio.**

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXfChI4oQS3PBGZ3feFOWCJ58gip8Y5pZXPDeO_aLXHSsr1MeA4KgqyPF7w_2EqVOnfbQTSDOkVdQhdNBLgRH6f4g_Rk0IgX7BwOA1HmzAb8GwNJn_0wRiqrHoZGRgJczkEnERLVxqQJXc2XcJu13BLqZbtc?key=5XBjb5S6ZTJgQPnoKOipBA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfChI4oQS3PBGZ3feFOWCJ58gip8Y5pZXPDeO_aLXHSsr1MeA4KgqyPF7w_2EqVOnfbQTSDOkVdQhdNBLgRH6f4g_Rk0IgX7BwOA1HmzAb8GwNJn_0wRiqrHoZGRgJczkEnERLVxqQJXc2XcJu13BLqZbtc?key=5XBjb5S6ZTJgQPnoKOipBA)

El comando **whois** es una herramienta esencial en el ámbito de la ciberseguridad y la administración de dominios. Permite obtener información sobre la propiedad y el estado de un dominio, lo que es crucial durante las fases de reconocimiento en pruebas de penetración y análisis de seguridad. En este caso, analizaremos el dominio josedomingo.org para extraer información relevante sobre su registro.

Campos relevantes de la salida de whois josedomingo.org:

- **Nombre del dominio** → josedomingo.org
- **ID del registro del dominio** → b89fa590095e43dfbc927551bcefc177-LROR
- **Servidor WHOIS del Registrador** → [http://whois.cdmon.com](http://whois.cdmon.com/) . El servidor WHOIS de registrador es un servicio que permite a los usuarios consultar información sobre el registro de nombres de dominio en Internet. Este servidor responde a las consultas realizadas utilizando el protocolo WHOIS, proporcionando detalles sobre la propiedad de un dominio, su estado y otros datos relevantes como estamos viendo.
- **URL del Registrador** → [http://www.cdmon.com](http://www.cdmon.com/)
- **Fecha de Creación** → 2005-10-04
- **Fecha de Actualización** → 2024-09-09
- **Fecha de Expiración** → 2025-10-04
- **Registrador** → Entidad autorizada que gestiona el registro de nombres de dominio en Internet, en el caso de josedomingo.org la entidad registrante es 10dencehispahard, S.L.
- **Estado del Dominio** → ok , significa que está activo, no hay problemas con el dominio y se encuentra registrado correctamente.
- **Organización del registrante** → Jose Domingo Munoz Rodriguez
- **Servidores de nombre** → ns1.cdmon.net, ns2.cdmon.net, ns3.cdmon.net, ns4.cdmondns-01.org, ns5.cdmondns-01.com (Estos son los servidores DNS que gestionan las resoluciones de nombre para el dominio josedomingo.org. Si un usuario intenta acceder a este dominio, su computadora enviará una consulta a uno de estos servidores DNS para obtener la dirección IP correspondiente.)
- **DNSSEC** → El dominio no está protegido por DNSSEC (Domain Name System Security Extensions). Esto implica que el dominio no cuenta con la seguridad adicional que protege contra ataques de suplantación de identidad.

### **2. Usad nslookup y dig para obtener toda la información posible de un dominio.**

**Herramienta nslookup**

Esta herramienta permite realizar consultas sobre los nombres de dominio y conocer cómo se resuelven en el sistema de nombres de dominio (DNS), así como a qué direcciones IP están apuntando.

En el siguiente código, se muestra cómo utilizar el comando `nslookup` para consultar el dominio **motogp.com**. Este comando devuelve la dirección IP del servidor asociado a este dominio, así como la información sobre el host desde el cual se ha ejecutado la consulta.

```html
nslookup motogp.com
```

Al ejecutar este comando, podemos observar la dirección IP asociada al dominio **motogp.com**, así como información adicional sobre la resolución DNS en el entorno local.

```html
Server:		100.100.1.1
Address:	100.100.1.1#53

Non-authoritative answer:
Name:	motogp.com
Address: 75.2.77.61
Name:	motogp.com
Address: 99.83.220.12

```

**Detalles de la salida**

**Servidor DNS utilizado:**

- **Server:** `100.100.1.1`
    - Este es el servidor DNS que se utilizó para realizar la consulta. La dirección IP indica que se está utilizando un servidor específico, en este caso, `100.100.1.1`.
- **Address:** `100.100.1.1#53`
    - La dirección IP del servidor se repite aquí, junto con el número `53`, que indica el puerto utilizado por el protocolo DNS.

**Respuesta no autoritativa:**

- **Non-authoritative answer:**
    - Esta sección indica que la respuesta proviene de un servidor DNS que no es autoritativo para el dominio consultado. Esto significa que el servidor no tiene la información directamente, sino que ha realizado la consulta a otros servidores DNS para obtener la respuesta.

**Nombre del dominio consultado:**

- **Name:** `motogp.com`
    - Esta es la consulta que se realizó, que en este caso es el dominio `motogp.com`.

**Direcciones IP asociadas:**

- **Address:** `75.2.77.61`
- **Address:** `99.83.220.12`
    - Aquí se muestran las direcciones IP a las que el dominio `motogp.com` está apuntando. Esto significa que el tráfico dirigido a `motogp.com` puede ser dirigido a cualquiera de estas dos direcciones IP.

Si solo usamos el comando nslookup, podemos ver lo siguiente:

![image.png](Pra%CC%81ctica%20Herramientas%20de%20seguridad%201299a2c89a9380d1ac6bdb2d22b7bdab/image%2048.png)

Esto que vemos por pantalla es una consola que nos abre el propio nslookup, al ejecutar el simple comando, por lo que se inicia el modo interactivo, por lo que se puede hacer lo siguiente:

1. Consultas de dominios.

En este caso le hemos hecho un nslookup a la dirección www.workshop.com.

![image.png](Pra%CC%81ctica%20Herramientas%20de%20seguridad%201299a2c89a9380d1ac6bdb2d22b7bdab/image%2049.png)

1. Comandos adicionales, o bien cambio de tipo de consultas.

![image.png](Pra%CC%81ctica%20Herramientas%20de%20seguridad%201299a2c89a9380d1ac6bdb2d22b7bdab/image%2050.png)

Para este ejemplo hemos cambiado el tipo de consulta a MX que nos muestra más información como la respuesta autorizada.

En este trozo de código:

```html
Non-authoritative answer:
[www.motogp.com](http://www.motogp.com/) canonical name = [www.amz.motogp.com](http://www.amz.motogp.com/).
```

Nos muestra lo siguiente: 

- El dominio `www.motogp.com` es un **nombre canónico** (CNAME, es un tipo de registro DNS que asigna un alias a un nombre de dominio auténtico) que apunta a `www.amz.motogp.com`

En la siguiente línea:

```html
[www.amz.motogp.com](http://www.amz.motogp.com/) canonical name = [d258nc2j26ec6i.cloudfront.net](http://d258nc2j26ec6i.cloudfront.net/).
```

- Indica que `www.amz.motogp.com` es, a su vez, un nombre canónico que apunta a `d258nc2j26ec6i.cloudfront.net`, lo que implica que el tráfico se redirige aún más hacia un servidor en la red de distribución de contenido (CDN)

En la línea:

```html
Authoritative answers can be found from:
[d258nc2j26ec6i.cloudfront.net](http://d258nc2j26ec6i.cloudfront.net/)
```

- Nos indican los servidores que tienen la información autoritativa sobre el dominio. En este caso, el nombre de dominio `d258nc2j26ec6i.cloudfront.net` es el que tiene la información DNS real y confiable para la consulta.

En la siguiente imagen, como anteriormente he comentado, nos aparece de manera interactiva la interfaz, por lo que vamos a escribir esta vez set type=NS y [lordsoftherings.com](http://lordsoftherings.com), para poder ver así los servidores de la página del señor de los anillos.

![image.png](Pra%CC%81ctica%20Herramientas%20de%20seguridad%201299a2c89a9380d1ac6bdb2d22b7bdab/image%2051.png)

---

**Herramienta DIG**

Dig es una herramienta de línea de comando que nos permite consultar información sobre dominios en el sistema DNS. 

Su uso:

- Consultar registros DNS.
- Diagnosticar problemas de resolución de nombres.
- Obtener detalles de las consultas.

Como podemos ver a continuación, he hecho una consulta a `www.dakar.com`

![image.png](Pra%CC%81ctica%20Herramientas%20de%20seguridad%201299a2c89a9380d1ac6bdb2d22b7bdab/image%2052.png)

En esta imagen podemos ver como saca información sobre los registros DNS, tanto de IPv4 como IPv6, registros MX (servidor de correo), el registro de la fecha y hora exacta a la que se hizo la petición.

### **3.** Usad DNSDumpster para obtener un esquema de los departamentos de una empresa.

DNS Dumpster es una herramienta totalmente gratuita online que proporciona servicios y herramientas relacionadas con la búsqueda de información en el historial de registros de DNS. Su función principal es rastrear y explorar el historial de registros DNS de un dominio específico.

Lo primero que observamos al abrir la web [https://dnsdumpster.com/](https://dnsdumpster.com/) es que tiene un estilo muy minimalista, lo primero que nos aparece es un buscador donde podemos poner el dominio que queramos, en mi caso voy a poner [josedomingo.org](https://fp.josedomingo.org/)

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXcvl4QLzqIubV6exSQ_x_gPay-s5AVzVsLSA101CnMj7KLV5fxfvp6NiPFFCy7INihWwu0ljU3DUZeBjHsZ1vyc-bWkESrFGSvCTnieWJgTo6NniuFMZOFiiYjWhVhwYtf6jcYJ-BGlGe8AisxCjan2XHw?key=YIp8DsEpTDKYA_gnisDf9A](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcvl4QLzqIubV6exSQ_x_gPay-s5AVzVsLSA101CnMj7KLV5fxfvp6NiPFFCy7INihWwu0ljU3DUZeBjHsZ1vyc-bWkESrFGSvCTnieWJgTo6NniuFMZOFiiYjWhVhwYtf6jcYJ-BGlGe8AisxCjan2XHw?key=YIp8DsEpTDKYA_gnisDf9A)

Una vez realizada la búsqueda lo primero que nos saldrá es el **Hosting** que muestra quienes son los propietarios de las direcciones IP que están alojando los servidores y subdominios del dominio.

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXcIFU-QMWwyphNC-uL06zPMtIQARhNbxymSgl3YnxbklWHoaWTGLG4uDyUzlsbrBW9fnKtWo-Hh36kIFMelGbqTe-NsMdmBZ605mjrb7dAQOiYzO2H5x3D69Y_hCOH1BVGaVi3I0HMmiY9kJCptet9420rR?key=YIp8DsEpTDKYA_gnisDf9A](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcIFU-QMWwyphNC-uL06zPMtIQARhNbxymSgl3YnxbklWHoaWTGLG4uDyUzlsbrBW9fnKtWo-Hh36kIFMelGbqTe-NsMdmBZ605mjrb7dAQOiYzO2H5x3D69Y_hCOH1BVGaVi3I0HMmiY9kJCptet9420rR?key=YIp8DsEpTDKYA_gnisDf9A)

Como observamos los propietarios de las IPs son Google cloud platform, Amazon, Zoho y OVH.

Lo siguiente que aparece son los servidores **DNS** que gestionan el dominio de josedomingo.org

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXddv6EZ-jfuiWQQ8YKJoqlCy1d4AtbEvZWbvnjYbO_UC74G-rhMGTTwg9tPXlR4MtYwMUZzg-ytlpfL252xMTYWyh6PxzK91ir_gRU6S0E5g2dCkJM0u1JSydvZRC68uYnDC7rAcpENLlcygO86oNKw400?key=YIp8DsEpTDKYA_gnisDf9A](https://lh7-rt.googleusercontent.com/docsz/AD_4nXddv6EZ-jfuiWQQ8YKJoqlCy1d4AtbEvZWbvnjYbO_UC74G-rhMGTTwg9tPXlR4MtYwMUZzg-ytlpfL252xMTYWyh6PxzK91ir_gRU6S0E5g2dCkJM0u1JSydvZRC68uYnDC7rAcpENLlcygO86oNKw400?key=YIp8DsEpTDKYA_gnisDf9A)

A continuación nos muestra los registros **MX**. Estos registros indican los servidores que gestionan el correo electrónico para josedomingo.org

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXdFKZ6SQnARLcrjsbpTEcyfgMEuVqUo8qquFwiRg24K_1qpnoHrzMZctomf0GAKYjJk8liujfXPn2G_x6Ze04l4oG_Gi1LQl_IvC0Rsdn1NIsU9iMZvARZbB39sTEwqDzwdK3bylGz3cueB_P-chyhY4Q1q?key=YIp8DsEpTDKYA_gnisDf9A](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdFKZ6SQnARLcrjsbpTEcyfgMEuVqUo8qquFwiRg24K_1qpnoHrzMZctomf0GAKYjJk8liujfXPn2G_x6Ze04l4oG_Gi1LQl_IvC0Rsdn1NIsU9iMZvARZbB39sTEwqDzwdK3bylGz3cueB_P-chyhY4Q1q?key=YIp8DsEpTDKYA_gnisDf9A)

Y por último nos aparece el **TXT Records** y el **Host records**.

Los registros TXT permiten asociar información adicional a un dominio.

Los registros Host records indican la dirección IP asociada con los diferentes subdominios de josedomingo.org, y qué tecnología de servidor HTTP están utilizando.

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXdADxJkyLQdMkaFbPCN2K5yt3LmaoRDVbMC-VjvnQ9Lu55E6impj-smGn-YDmjDIHF02Q0nA3QpxMDbrwUKMGd3G6qv-DEVDkJeSwq_l9cZZSr7sZj1PkEZsbsXeiY8XKzVFSGoaNI5B9z45lTqIWPNlWA9?key=YIp8DsEpTDKYA_gnisDf9A](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdADxJkyLQdMkaFbPCN2K5yt3LmaoRDVbMC-VjvnQ9Lu55E6impj-smGn-YDmjDIHF02Q0nA3QpxMDbrwUKMGd3G6qv-DEVDkJeSwq_l9cZZSr7sZj1PkEZsbsXeiY8XKzVFSGoaNI5B9z45lTqIWPNlWA9?key=YIp8DsEpTDKYA_gnisDf9A)

Y por último tenemos un mapa visual de la infraestructura del dominio, mostrando cómo los diferentes servidores y subdominios están conectados entre sí.

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXd6y9BvHhNfMyIUDpGmxaJeYMF-dfo9qIOP-fFBITxJh-4Y_7JZTpN8KD0qkCrE7nzErxthft1NeAz9yyiigZBQ_PGK0xbaBrglhgQOqB9OTPEqV3SeW62BfX7e-gr-JrS4rp5g1Cr_KWQ4BV11aPvx3Jul?key=YIp8DsEpTDKYA_gnisDf9A](https://lh7-rt.googleusercontent.com/docsz/AD_4nXd6y9BvHhNfMyIUDpGmxaJeYMF-dfo9qIOP-fFBITxJh-4Y_7JZTpN8KD0qkCrE7nzErxthft1NeAz9yyiigZBQ_PGK0xbaBrglhgQOqB9OTPEqV3SeW62BfX7e-gr-JrS4rp5g1Cr_KWQ4BV11aPvx3Jul?key=YIp8DsEpTDKYA_gnisDf9A)

### 4. Intentad localizar con Shodan las máquinas expuestas por una empresa.

**Introducción**

Shodan es un motor de búsqueda especializado en identificar dispositivos conectados a Internet, tales como servidores, routers, cámaras de seguridad, bases de datos, sistemas de control industrial (ICS), dispositivos IoT, y más. A diferencia de los motores de búsqueda tradicionales como Google, que indexan sitios web y su contenido, Shodan busca información sobre los servicios y puertos abiertos de dispositivos, lo que permite ver si están expuestos a la red pública y qué tipos de vulnerabilidades podrían presentar.

**¿Cuál es la finalidad de Shodan?**

Básicamente Shodan realiza un escaneo constante de Internet en busca de dispositivos o servicios que sean accesibles. En caso de encontrar vulnerabilidades, recopila información útil y la indexa.

**Primeros pasos con Shodan**

Antes de empezar a realizar búsquedas, tendremos que registrarnos en la página de [S**hodan**](https://shodan.io/):

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXfoeu-KpCLtrZuiMmVNmMtDUhKZWWyoT8acNgPBXr59nadbdMHUCoUgdxZxq_2cOcEJswI4bDrUdWXi0aQrUXdBdN19fRC-i6tX6SHHRkPX3LDB12ctHg2dmrQYrge5f3Iu_b3g3PIoEYo0OT5XxO7zpqq4?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfoeu-KpCLtrZuiMmVNmMtDUhKZWWyoT8acNgPBXr59nadbdMHUCoUgdxZxq_2cOcEJswI4bDrUdWXi0aQrUXdBdN19fRC-i6tX6SHHRkPX3LDB12ctHg2dmrQYrge5f3Iu_b3g3PIoEYo0OT5XxO7zpqq4?key=amEUHfTdJnvQeZF3EjeoeA)

Para empezar a hacer búsquedas antes debemos saber que Shodan utiliza filtros (aunque no sea completamente necesario). Por ejemplo, algunos de los filtros que nos pueden interesar:

`country:<código>`: Filtra resultados por país.

- Ejemplo: country:ES (España)

`city:<nombre>`: Filtra resultados por ciudad.

- Ejemplo: city:Sevilla

`hostname:<nombre>`: Filtra resultados por el nombre de host.

- Ejemplo: hostname:empresa.com

`org:<nombre>`: Filtra resultados por organización.

- Ejemplo: org:Google

`port:<número>`: Filtra resultados por puerto específico.

- Ejemplo: port:80 (HTTP)

`product:<nombre>`: Filtra resultados por producto o software específico.

- Ejemplo: product:Apache

`version:<número>`: Filtra resultados por versión de un software.

- Ejemplo: version:2.4.41 (versión específica de Apache)

`os:<nombre>`: Filtra resultados por sistema operativo.

- Ejemplo: os:Windows

`vuln:<CVE>`: Filtra resultados por una vulnerabilidad específica.

- Ejemplo: vuln:CVE-2019-11510

`net:<dirección>`: Filtra resultados por rango de dirección IP.

- Ejemplo: net:192.168.1.0/24

`before:<fecha> y after:<fecha>`: Filtran resultados basados en la fecha en que se realizó el escaneo.

- Ejemplo: before:2023-01-01

`has_screenshot`: Filtra resultados que tienen una captura de pantalla disponible.

- Ejemplo: has_screenshot

`tags:<etiqueta>`: Filtra resultados por etiquetas asignadas a los dispositivos.

- Ejemplo: tags:default

Antes de empezar a usar los filtros y hacer búsquedas más precisas, haré una pequeña comprobación con el instituto. Podemos hacer la búsqueda con la IP o con su dominio, por ejemplo, voy a hacerlo con la IP:

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXevtJYL4SZ0fdHpeg9VyiTHS7HGQRuctvtPPkNOuRN6XtcIuYhbkMbK31jMJoBt5tuaECoprI-FzMuPX4NwnGmoD29XAslQrnhWkzsFi6GxT26mGq_ypDiQFuXNaDtgyRsnk4NElQKV_XfWL3xwIhgtyHU?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXevtJYL4SZ0fdHpeg9VyiTHS7HGQRuctvtPPkNOuRN6XtcIuYhbkMbK31jMJoBt5tuaECoprI-FzMuPX4NwnGmoD29XAslQrnhWkzsFi6GxT26mGq_ypDiQFuXNaDtgyRsnk4NElQKV_XfWL3xwIhgtyHU?key=amEUHfTdJnvQeZF3EjeoeA)

Pegamos la IP del nombre `dit.gonzalonazareno.org` en el buscador

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXdMLitcHlhI_45GKYqxfngylvtylNmg5SzvV1M4TGW4eto2iBRRbn6AcvUaBvWRmMG3xAuDnzbSvWhf2ubhZ3fLzMvxtCyOeURWtoR8GWJH3EROrbe4D7jvy6mKdHvLq6wWhz2t36wnJMR6o18JlXsilFR3?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdMLitcHlhI_45GKYqxfngylvtylNmg5SzvV1M4TGW4eto2iBRRbn6AcvUaBvWRmMG3xAuDnzbSvWhf2ubhZ3fLzMvxtCyOeURWtoR8GWJH3EROrbe4D7jvy6mKdHvLq6wWhz2t36wnJMR6o18JlXsilFR3?key=amEUHfTdJnvQeZF3EjeoeA)

En la parte izquierda nos muestra información general:

- El servidor está ubicado físicamente en Lille (Francia).
- Utiliza OVH como infraestructura.
- El ASN 16276 pertenece a OVH y gestiona un gran número de direcciones IP, por lo que es una red robusta.

En la parte superior derecha nos mostrará todos los puertos abiertos y servicios que se ejecutan en ellos. Y además, hay una parte de información muy importante que es la fecha más reciente en que Shodan escaneó y registró información sobre este servidor. 

Esto, en caso de que queramos hacer un ataque ***(ojo porque es ilegal)*** es importante, pues si encontramos una máquina expuesta de hace un año por ejemplo, posiblemente ya no esté disponible o ha dejado de estar expuesta.

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXezFkYidTlTUTPEydthqn6-BUsd9e0HEFjKYm11V9MDPLttEPzw2IjeZmhlqntXSiReI9CZ50g8rdH8ohCxY9GqWZJkBtIsiRRdsMJatE8rd0aVweRkelC90u0cht8iTIUrn6oWgIDbQizsMzK12pzWCgcB?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXezFkYidTlTUTPEydthqn6-BUsd9e0HEFjKYm11V9MDPLttEPzw2IjeZmhlqntXSiReI9CZ50g8rdH8ohCxY9GqWZJkBtIsiRRdsMJatE8rd0aVweRkelC90u0cht8iTIUrn6oWgIDbQizsMzK12pzWCgcB?key=amEUHfTdJnvQeZF3EjeoeA)

Si seguimos bajando podemos encontrar algunos detalles adicionales, por ejemplo:

- Banners de servicios

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXd1sX320Sq5TP3hmEnhQE8MMXjyl2gLh8kNvdU-rV2M03f6g7m-KYZKijLDVsoeYLaRxyGV72e9JZDFLYaX51S5oRDMEgogg7x7-rrKPuA600wJDFnlTFhxarIzrbu2LsVKgcHlDdMWwQT5LfoHgxxB35Zs?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXd1sX320Sq5TP3hmEnhQE8MMXjyl2gLh8kNvdU-rV2M03f6g7m-KYZKijLDVsoeYLaRxyGV72e9JZDFLYaX51S5oRDMEgogg7x7-rrKPuA600wJDFnlTFhxarIzrbu2LsVKgcHlDdMWwQT5LfoHgxxB35Zs?key=amEUHfTdJnvQeZF3EjeoeA)

- Certificados SSL/TLS si están presentes

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXciIfoVUOoGrAUcQsGuAVpaQpIz8qBwnwOqbaMauT5BwcFGZWq5OWnP2S7MAjN6McB9aYVCojWufEHUKaHejtfgg5SkuIsyuUgFTeH_uzq11GSj2z3jMRgaXj1AMTp_hUVTRVeMRV9LhuM6PAAjP_YvW78?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXciIfoVUOoGrAUcQsGuAVpaQpIz8qBwnwOqbaMauT5BwcFGZWq5OWnP2S7MAjN6McB9aYVCojWufEHUKaHejtfgg5SkuIsyuUgFTeH_uzq11GSj2z3jMRgaXj1AMTp_hUVTRVeMRV9LhuM6PAAjP_YvW78?key=amEUHfTdJnvQeZF3EjeoeA)

- Posibles vulnerabilidades conocidas asociadas a las versiones de software detectadas

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXdDHx9KVUawwSM5l6YVFQgAqw-tl2jHuxb8_GJ4FARGYNRv91djxAuqC574bfI5ulWdrHZ9w8fa014AeC_qBQR1pYgtgCTAhA26Qp5Rl_uUqSLkIHDJ1htQpMOvzpLJVdhyofWTtFppbzZQLZ-vn-7dfpA?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdDHx9KVUawwSM5l6YVFQgAqw-tl2jHuxb8_GJ4FARGYNRv91djxAuqC574bfI5ulWdrHZ9w8fa014AeC_qBQR1pYgtgCTAhA26Qp5Rl_uUqSLkIHDJ1htQpMOvzpLJVdhyofWTtFppbzZQLZ-vn-7dfpA?key=amEUHfTdJnvQeZF3EjeoeA)

Es importante tener en cuenta que la información mostrada por Shodan se limita a lo que está públicamente accesible y puede variar dependiendo de la configuración de seguridad del servidor. 

Además, la información puede no estar completamente actualizada, ya que Shodan realiza escaneos periódicos pero no en tiempo real.

**Búsquedas con filtros**

Bien, ahora que sabemos un poco como funciona Shodan, voy a proceder a realizar búsquedas para encontrar máquinas expuestas. Por ejemplo:

```powershell
ssh port:22,3333 country:ES city:"Sevilla"
```

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXc5_DjtL860BqGk-ykR43L3R0yZXqaPmF10n4Ge6EfFVK8soXEG7fCdkcGSgSt-kaPNA0RF5I_wdBvA7QDc4OKfC02TQDYOdgROtOk4RRmoFUCAGegLkmT8CGoGXwWGZ912mHBzXJngvU4euI83QLmvP3A?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXc5_DjtL860BqGk-ykR43L3R0yZXqaPmF10n4Ge6EfFVK8soXEG7fCdkcGSgSt-kaPNA0RF5I_wdBvA7QDc4OKfC02TQDYOdgROtOk4RRmoFUCAGegLkmT8CGoGXwWGZ912mHBzXJngvU4euI83QLmvP3A?key=amEUHfTdJnvQeZF3EjeoeA)

En este filtro estoy buscando máquinas expuestas que estén utilizando el servicio SSH en el puerto 22 y 3333, este último es menos común pero también puede estar configurado para SSH. Aparte, estoy buscando máquinas en España, concretamente Sevilla.

Como podemos observar en la imagen se han encontrado 3253, si accedemos a una de ellas:

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXcM_K-vUlOnM-3fH29G_enKH5dpr8DXjvwwNKxjLw1ZWtVU7UfBFU7xvxwsa-TjzKjGMzrzJCCvwM8XMCIlIW5txj0PiZMtJIYMg7AnM-9YN2P0mCRvyrbzZNFjbeFmYMz9H-1wp3eW5urrJDybf9mxbHnw?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcM_K-vUlOnM-3fH29G_enKH5dpr8DXjvwwNKxjLw1ZWtVU7UfBFU7xvxwsa-TjzKjGMzrzJCCvwM8XMCIlIW5txj0PiZMtJIYMg7AnM-9YN2P0mCRvyrbzZNFjbeFmYMz9H-1wp3eW5urrJDybf9mxbHnw?key=amEUHfTdJnvQeZF3EjeoeA)

Esto nos mostrará la información que hemos explicado antes. Al parecer, se trata de la organización “**TELEFONICA DE ESPANA S.A.U**.”, y lo más importante es que nos muestra toda la información:

- Se trata de una máquina Dropbear, el cual es un servidor SSH ligero y de bajo consumo, que es común en entornos de recursos limitados.
- Last Seen: 2024-10-23: esto significa que el último escáner fue hoy mismo.
- Claves y Algoritmos:
    - **Key type**: ssh-rsa
    - **Fingerprint**: 5d:27:b4:1d:59:70:c9:ae:71:72:d3:3c:a7:c4:bd:6c
    - **Kex Algorithms**: Utiliza el algoritmo de intercambio de claves Diffie-Hellman.
    - **Server Host Key Algorithms**: Incluye ssh-rsa y ssh-dss.
    - **Encryption Algorithms**: Lista de algoritmos de cifrado soportados, incluyendo AES y 3DES, algunos de los cuales son más seguros que otros.
    - **MAC Algorithms**: Algoritmos de código de autenticación de mensajes, que protegen la integridad de la conexión.
    - **Compression Algorithms**: Algoritmos de compresión disponibles.

Ahora, voy a hacer una búsqueda parecida a la anterior pero con los protocolo RDP y SMB, comúnmente utilizados en Windows, para ello:

```powershell
port:3389
```

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXeFtGe0YEPh45AZKLkYrJtS9yXg4ZHxxRt8D90YzKn5mB388e7Ha_TP-ek8p33zdm-umEczMVrCzeqctMsGohV5HcaVU9iSAqYl-w43nQeHu6yj23gUisUirpGvNnjLK3j54e57n3UIsyCCZa5EwpJ8ChDV?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeFtGe0YEPh45AZKLkYrJtS9yXg4ZHxxRt8D90YzKn5mB388e7Ha_TP-ek8p33zdm-umEczMVrCzeqctMsGohV5HcaVU9iSAqYl-w43nQeHu6yj23gUisUirpGvNnjLK3j54e57n3UIsyCCZa5EwpJ8ChDV?key=amEUHfTdJnvQeZF3EjeoeA)

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXeRLzEAwNJRWJGGDNw8Ywo7PL70vVUyzMOR4lF4-ZnwsZsTk9Ikp4cWi6Df1I61UCMnBvs5tYRdoDQsRVqwQzGYzE75T9QU7hwD-SjoXO7-Ax3WcX4pF1QD3Qgbd8s7fKPbG2vfiM_pl-yRv5gZyhssGxSV?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeRLzEAwNJRWJGGDNw8Ywo7PL70vVUyzMOR4lF4-ZnwsZsTk9Ikp4cWi6Df1I61UCMnBvs5tYRdoDQsRVqwQzGYzE75T9QU7hwD-SjoXO7-Ax3WcX4pF1QD3Qgbd8s7fKPbG2vfiM_pl-yRv5gZyhssGxSV?key=amEUHfTdJnvQeZF3EjeoeA)

**Información de RDP**:

- **OS**: Windows 10 (version 1809) / Windows Server 2019 (version 1809)
- **OS Build**: 10.0.17763
    - Esta es la identificación específica de la versión de Windows.
- **Target Name**: JCCO
- **NetBIOS Domain Name**: JCCO
- **NetBIOS Computer Name**: JCCO-APP01
    - Indica el nombre de la máquina dentro del dominio.
- **DNS Domain Name**: jcco.com
- **DNS Tree Name**: jcco.com
- **FQDN**: JCCO-APP01.jcco.com
    - El Nombre de Dominio Completo, lo que significa que la máquina puede ser fácilmente identificada en la red.

Por último, mostraré como también se puede acceder a las webcams de algunas máquinas que hayan sido expuestas. Los filtros los he encontrado en este repositorio → [https://github.com/jakejarvis/awesome-shodan-queries?tab=readme-ov-file#webcams](https://github.com/jakejarvis/awesome-shodan-queries?tab=readme-ov-file#webcams)

```powershell
("**webcam 7" OR "webcamXP**") http.component:"mootools" -401
```

El filtro busca dispositivos que utilizan software de cámaras web específicas, como Webcam 7 o webcamXP, que son comunes para la transmisión de video desde cámaras IP. Al incluir `http.component:"mootools"`, se limita a aquellos que usan MooTools, una biblioteca JavaScript que puede indicar ciertas características o vulnerabilidades en la interfaz. El `**-401**` excluye resultados que requieren autentificación, lo que significa que son webcams que son accesibles sin necesidad de credenciales.

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXcstj2FgwHHW2RtRjtrYlm5BLsgiWE24E9FbdBKHIuijbMuJB8OPXLKoucOUeqQEzgPK4dSBSqG1qeUWHs0OZTkRoXlzW6Ka4fefcmYydNgl7HAoWjB0sw9Qu7XeVDagxcqiCxjmn9gJmODIixHtlpm2NQ6?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcstj2FgwHHW2RtRjtrYlm5BLsgiWE24E9FbdBKHIuijbMuJB8OPXLKoucOUeqQEzgPK4dSBSqG1qeUWHs0OZTkRoXlzW6Ka4fefcmYydNgl7HAoWjB0sw9Qu7XeVDagxcqiCxjmn9gJmODIixHtlpm2NQ6?key=amEUHfTdJnvQeZF3EjeoeA)

Por ejemplo, he accedido a una de las máquinas y he podido ver la grabación en directo, adjunto imagen:

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXeSk8YvpBX85IEn4RcRFStu4j4cTAy6uQ-miQErlO2TVIY4HhdN7KtrUZsjKI_upMpvdx2K06WD8ewg4Yx2SJDH1wpvXSt8mrOWLXfcjuvotlBWRQuAsQ33oFvlZFzQ9O8BE-aLee8Zn0zV9jFrnaaLzLY?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeSk8YvpBX85IEn4RcRFStu4j4cTAy6uQ-miQErlO2TVIY4HhdN7KtrUZsjKI_upMpvdx2K06WD8ewg4Yx2SJDH1wpvXSt8mrOWLXfcjuvotlBWRQuAsQ33oFvlZFzQ9O8BE-aLee8Zn0zV9jFrnaaLzLY?key=amEUHfTdJnvQeZF3EjeoeA)

## Reconocimiento activo

### **5. Utilizad Wappalyzer para obtener información del Gonzalo Nazareno.**

Wappalyzer es una herramienta que permite identificar las tecnologías utilizadas en los sitios web. En este ejercicio, presentaremos el análisis del sitio gonzalonazareno.org, donde recopilaremos información sobre su stack tecnológico, así como sobre aspectos de seguridad y rendimiento.

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXfPvw2mjBO4v6TDmEbBmJuqedoyfaN2A2DYnNDYsT91LCXDelMg-8KjKoPIrwMpAhJnXyFsUjkfBoC0SNhNGYWeADzT8jXSjRbQ2Ri9GCDKRCrJy3HlodIeH6kcZ3hzcPdsw1anISpHUePnangn20x4OFRy?key=5XBjb5S6ZTJgQPnoKOipBA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfPvw2mjBO4v6TDmEbBmJuqedoyfaN2A2DYnNDYsT91LCXDelMg-8KjKoPIrwMpAhJnXyFsUjkfBoC0SNhNGYWeADzT8jXSjRbQ2Ri9GCDKRCrJy3HlodIeH6kcZ3hzcPdsw1anISpHUePnangn20x4OFRy?key=5XBjb5S6ZTJgQPnoKOipBA)

Información sobre el stack tecnológico del sitio web gonzalonazareno.org:

- **Lenguajes de Programación**:
    - Python: El sitio utiliza Python como lenguaje de programación principal.
- **Proxies Inversos**:
    - Nginx (1.14.2): Nginx se emplea como proxy inverso, mejorando la capacidad de manejo de las solicitudes de los usuarios y optimizando la entrega de contenido.
- **Frameworks de Interfaz de Usuario (UI)**:
    - Bootstrap (3.3.7): Este framework facilita el diseño responsivo y atractivo del sitio, permitiendo una mejor experiencia para los usuarios en diferentes dispositivos.
- **Frameworks Web**:
    - Django: Utiliza Django, un poderoso framework de Python, que permite un desarrollo web rápido y seguro.
- **Servidores Web**:
    - Nginx (1.14.2): Además de ser un proxy inverso, Nginx actúa como el servidor web principal, gestionando las solicitudes HTTP.
- **Red de Entrega de Contenidos (CDN)**:
    - Google Hosted Libraries: Esta CDN ayuda a cargar bibliotecas JavaScript rápidamente, mejorando la velocidad de carga del sitio.
- **Bibliotecas de JavaScript**:
    - jQuery (1.9.1): jQuery se utiliza para facilitar la manipulación del DOM y mejorar la interacción del usuario en el frontend.

Información sobre la seguridad del sitio web gonzalonazareno.org:

- **HSTS (HTTP Strict Transport Security)**: Indica que el sitio está configurado para ser accedido únicamente a través de HTTPS, lo que mejora la seguridad de la información de los usuarios y protege contra ataques de tipo "man-in-the-middle".
- **SSL/TLS**: El sitio cuenta con certificados SSL/TLS habilitados, lo que significa que las comunicaciones entre el navegador del usuario y el servidor están encriptadas.

### 6. Buscad la utilidad del comando nc y aplicadlo en un caso concreto.

Cuando hablamos del comando `nc` también lo podemos conocer como `netcat`, es una herramienta de línea de comando (a través de consola) la cual se usa paras leer y escribir datos a través de conexiones de red usando tanto el protocolo TCP como UDP.

- TCP —>Protocolo que nos garantiza la entrega correcta y ordenada de datos
- UDP —> Protocolo sin conexión y más rápido, pero no asegura la entrega ni el orden de datos.

Se puede considerar una herramienta que es bastante flexible y poderosa que nos permite:

1. Enviar archivos desde un sistema a otro usando el siguiente comando:

`nc -w 3 [dirección IP destino] [puerto] < archivo.txt`

Desglose de este comando:

- `nc`: Es el comando netcat.
- `w 3`: Establece un timeout de espera de 3 segundos para la conexión.
- `[dirección IP destino]`: Aquí debes reemplazar con la dirección IP del destino al que deseas enviar el archivo.
- `[puerto]`: Reemplaza con el número de puerto en el destino.
- `< archivo.txt`: Redirige el contenido del archivo `archivo.txt` a la entrada de `nc`.

1. Realización de pruebas de conectividad.

Por ejemplo, comprobar si un servidor determinado esta escuchando en un puerto especifico usando el siguiente comando:

`echo "GET /" | nc [dirección IP servidor] [puerto]`

Desglose de este comando:

- `echo "GET /"`: Envía el texto `GET /`, que es una solicitud HTTP GET simple para la raíz del servidor.
- `|`: Este es un pipe que toma la salida del comando `echo` y la redirige como entrada al siguiente comando.
- `nc [dirección IP servidor] [puerto]`: Ejecuta `nc` con la dirección IP del servidor y el puerto especificado. Aquí, debes reemplazar `[dirección IP servidor]` con la dirección IP real del servidor al que deseas conectarte, y `[puerto]` con el puerto correspondiente.

1. Creación de túneles a través de proxies.

Como ejemplo  si queremos acceder a un servicio en el puerto 8080 de un servidor interno a través de un proxy en el puerto  8888, usaremos este comando que pondré a continuación:

`nc -X connect -x [dirección IP proxy]:[puerto proxy] [dirección IP servidor interno] 8080`

Pero si nos vamos a un caso en concreto lo primero que se nos viene a la mente es ver que puertos están disponible para poder atacar, por lo que el comando más útil y efectivo es el siguiente:

`nc -zv <ip> <nº puertos>`

Lo vamos a probar con una máquina que tengo en mi escritorio, y vamos a prceder, para ello el comando en cuestión es:

`adandy@toyota-hilux:~$ nc -zv 172.22.7.101 1-8888`

- **`nc`**: Llama a netcat, una herramienta de red que puede leer y escribir datos a través de conexiones de red utilizando TCP o UDP.
- **`z`**: Indica que se debe realizar un escaneo de puertos (modo "zero-I/O"). Este flag se usa para hacer pruebas de conexión sin enviar datos.
- **`v`**: Activa el modo verbose (detallado), mostrando más información sobre lo que está sucediendo.
- **`172.22.7.101`**: La dirección IP de la máquina que se está escaneando.
- **`1-8888`**: Especifica el rango de puertos que se están escaneando, desde el puerto 1 hasta el puerto 8888.

Y como vemos a continuación, nos sale en la pantalla lo siguiente:

![image.png](Pra%CC%81ctica%20Herramientas%20de%20seguridad%201299a2c89a9380d1ac6bdb2d22b7bdab/image%2053.png)

Ahora proceder a desglosar lo que ha ocurrido, es decir el resultado del comando:

Como vemos a todo por pantalla nos da **“Connection refused”**, lo cual nos indica que nc intenta conectarse a los puertos en este caso desde el 1 al 21, pero no encontró ningún servicio que escuche dichos puertos.

Pero vamos que en el puerto 22, nos dice lo siguiente **"Connection to 172.22.7.101 22 port [tcp/ssh] succeeded!",** el cual nos dice que nc logro establecer una conexión con el puerto 22, que es el puerto que se usa para la conexión SSH. 
Por lo que esta este puerto esta abierto y accesible, para un posible ataque o entrada.

### 7. Buscad la forma de utilizar el comando nmap para conocer las máquinas de una red usando ARP Scan y explica en qué se basa su funcionamiento capturando el tráfico generado con Wireshark.

Nmap es una herramienta de escaneo de redes que permite descubrir hosts y servicios en una red.

```powershell
sudo nmap -PR 192.168.1.0/24
```

Este comando lo que hace es:

- **PR**: Esta opción indica a nmap que realice un escaneo de tipo ARP. Este método envía paquetes ARP a la red para determinar qué dispositivos están activos. El escaneo ARP es efectivo en redes locales ya que el protocolo ARP es utilizado para resolver direcciones IP a direcciones MAC en la misma red.
- **192.168.1.0/24**: Esta es la dirección de red y la máscara de subred que indica que se escanearán todas las direcciones IP en el rango de 192.168.1.1 a 192.168.1.254.

En el resultado del comando, se puede observar una lista de las máquinas activas en la red, junto con sus direcciones IP, direcciones MAC y algunos puertos abiertos.

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXeyKKAnnPtPGUTFKN_rwVvNPiJPBUBGchPMgsUzNlxAqad2B_zInZ-vgIZy2Aoayq9Z8IusE8V4zfb9Z0aJEjVDRfHhwUTNm4di7L82BClESBV3sDyf-mkE_uhnrldAXASapxd7zjUWRtntIBHfdF-P-Xk?key=5XBjb5S6ZTJgQPnoKOipBA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeyKKAnnPtPGUTFKN_rwVvNPiJPBUBGchPMgsUzNlxAqad2B_zInZ-vgIZy2Aoayq9Z8IusE8V4zfb9Z0aJEjVDRfHhwUTNm4di7L82BClESBV3sDyf-mkE_uhnrldAXASapxd7zjUWRtntIBHfdF-P-Xk?key=5XBjb5S6ZTJgQPnoKOipBA)

Cuando nmap realiza un ARP scan , envía un ARP request preguntando a toda la red (broadcast) "¿Quién tiene la dirección IP X.X.X.X? Dime tu dirección MAC". En este caso manda 256 ARPs request, uno por cada una de las direcciones posibles dentro de la red 192.168.1.0/24.

Los host que tengan direccionamiento ip asignado dentro de la red contestaran a dicho arp request con un arp reply en el que indicarán su dirección mac

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXdGBLqQlvoUwTdRBv6olJxorzr-Sr4DcDmlme2f1NGo_QYAg3E5hzzv8gKFBhwJptpW4Eqfh7A7i2MWqNsUZ6EzCfNT8p4O8VdtZoL9c1N4bzfIDtf1Fcl7thLvZeW8ZwXhgN9uK2ojNRRZLiVv9GI9_Ck?key=5XBjb5S6ZTJgQPnoKOipBA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdGBLqQlvoUwTdRBv6olJxorzr-Sr4DcDmlme2f1NGo_QYAg3E5hzzv8gKFBhwJptpW4Eqfh7A7i2MWqNsUZ6EzCfNT8p4O8VdtZoL9c1N4bzfIDtf1Fcl7thLvZeW8ZwXhgN9uK2ojNRRZLiVv9GI9_Ck?key=5XBjb5S6ZTJgQPnoKOipBA)

**Frame de un ARP request:**

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXdjkhB3LAFCiHYB1QEvKgfKmbfGvw6p1PMejbj4LZrUlYb7ux9P3IVUUNCEW4lIbmyGXky1eDhLjoO2QRpCOqFI9yUOIC5l5C_rQ-UhLA88kj9vmxTC9L6waVfhnhxpKiw5k2_FCFy0p24thE-1bKDjQe1H?key=5XBjb5S6ZTJgQPnoKOipBA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdjkhB3LAFCiHYB1QEvKgfKmbfGvw6p1PMejbj4LZrUlYb7ux9P3IVUUNCEW4lIbmyGXky1eDhLjoO2QRpCOqFI9yUOIC5l5C_rQ-UhLA88kj9vmxTC9L6waVfhnhxpKiw5k2_FCFy0p24thE-1bKDjQe1H?key=5XBjb5S6ZTJgQPnoKOipBA)

Vemos que es un mensaje de broadcast que se está mandando a toda la red y si algún host en la red tiene asignado dicha dirección ip contestará con el correspondiente ARP reply.

**Frame de un ARP reply:**

Aquí vemos el caso de como uno de los 256 arp request que se han mandado ha recibido su correspondiente respuesta en forma de arp reply. En la respuesta dicho host indica su dirección mac.

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXcNDaHYdHiozyPQ8yLtGUBSjp3AhE7z_rCxtDRHGuSPmHYM9sYgrB4MJoAwTExvmYocXCNgNliUEZmJBk708z5bXYCgjDIg2KHzvCCmulDTInQjBtl5ebi2ismzxrNadp0jwad5WL2-O7mSO7WcfkTNUFPJ?key=5XBjb5S6ZTJgQPnoKOipBA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcNDaHYdHiozyPQ8yLtGUBSjp3AhE7z_rCxtDRHGuSPmHYM9sYgrB4MJoAwTExvmYocXCNgNliUEZmJBk708z5bXYCgjDIg2KHzvCCmulDTInQjBtl5ebi2ismzxrNadp0jwad5WL2-O7mSO7WcfkTNUFPJ?key=5XBjb5S6ZTJgQPnoKOipBA)

También se usan las opciones -sV para escanear todos los puertos de un dispositivo con el servicio y la versión para luego poder atacarlos.

### **8. Buscad la forma de utilizar el comando nmap para conocer las máquinas de una red usando ICMP Scan y explica en qué se basa su funcionamiento capturando el tráfico generado con Wireshark.**

**Nmap** sirve para obtener información, con cierto nivel de detalle, acerca de todos los dispositivos conectados en el sistema.

Un escaneo de red con **Nmap** incluye tanto **routers como ordenadores** y datos sobre la tecnología de cada uno, por lo que, **Nmap** sirve para **encontrar vulnerabilidades informáticas en los sistemas** y determinar qué vector de ataque podría aprovechar un hacker malicioso.

Por ejemplo, vamos a hacer un escaneo de la red del instituto:

```powershell
nmap -sn -PE 172.22.12.0/24
```

- **-sn:** Desactiva el escaneo de puertos, realizando solo descubrimiento de hosts
- **-PE:** Habilita el sondeo ICMP Echo (ping) ****COMPROBAR SI HACE ALGO EL -PE**

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXfmRUZZFH-mtz6nDNSMwMTQpAVTPj9EUJS8U7wz8SSwEHVeSUFnHKN72KOvGy4ttfguxJPvJlV3Z4nbir0UYg6yc7kAvQhy0X2EGZzuyO8kVWvGg5PpX46WgGXUkPT476jkjwWEcmQiXvUtviL8bW6vX9Db?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfmRUZZFH-mtz6nDNSMwMTQpAVTPj9EUJS8U7wz8SSwEHVeSUFnHKN72KOvGy4ttfguxJPvJlV3Z4nbir0UYg6yc7kAvQhy0X2EGZzuyO8kVWvGg5PpX46WgGXUkPT476jkjwWEcmQiXvUtviL8bW6vX9Db?key=amEUHfTdJnvQeZF3EjeoeA)

**Nota:** En este caso lo hicimos con **/24** porque esta dispone de menos máquinas conectadas.

El resultado del **escaneo ICMP** que hemos realizado con Nmap nos muestra los hosts activos en la subred `172.22.12.0/24`. En total, se han detectado seis hosts activos, que son:

`172.22.12.9, 172.22.12.23, 172.22.12.34, 172.22.12.48, 172.22.12.50` y la propia máquina desde donde estoy haciendo el escaneo, `172.22.12.28`.

Los **tiempos de respuesta** de los hosts son muy **bajos**, lo que **indica** que todos los dispositivos están en la **misma red local** y **responden rápidamente** a las solicitudes ICMP. Si nos damos cuenta, tres de los hosts `(172.22.12.9, 172.22.12.23 y 172.22.12.34)` tienen direcciones **MAC desconocidas**, lo que podría decirnos que son dispositivos menos comunes o que Nmap no tiene información actualizada sobre ellos.

Dos de los **hosts detectados** `(172.22.12.48 y 172.22.12.50)` comparten la **misma** dirección **MAC** `(00:11:22:68:27:B6)`, que **pertenece a Cimsys**.

El **escaneo** ha abarcado un total de **256 direcciones IP** y ha encontrado solo ***seis hosts activos.*** Básicamente esto es porque en esta red, la mayoría de dispositivos están conectados a otra netmask, en este caso la `/16`.

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXdsNgMPtlzhxJSHQSCwqUZU0oXgXU0z9seF-K3bqMc7fLvl8xlvOi1OpbAVnpTC6dg7LQvnnD6j8WJkc_EO6FrCj5-lbvw2AMgr_H4Rkz_b9WSwTNqSNV74cbtAr-BMXwiUjhQPP7r7xfJiMmpXGavrqZLw?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdsNgMPtlzhxJSHQSCwqUZU0oXgXU0z9seF-K3bqMc7fLvl8xlvOi1OpbAVnpTC6dg7LQvnnD6j8WJkc_EO6FrCj5-lbvw2AMgr_H4Rkz_b9WSwTNqSNV74cbtAr-BMXwiUjhQPP7r7xfJiMmpXGavrqZLw?key=amEUHfTdJnvQeZF3EjeoeA)

### **9. Buscad la forma de identificar los servicios que ofrece una máquina usando en nmap la técnica TCP SYN Ping y haz una pequeña prueba sobre una MV con Postgres accesible desde la tuya. Explicad en qué se basa su funcionamiento usando Wireshark.**

Para la prueba hemos utilizado una máquina virtual con un servidor Postgre con direccionamiento 192.168.122.164:

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXcAcdIsr3VuolKVsO4XpKcsdawZVSZHUEcTC5hY8MTyPIgWA5bK67DSnb7FIqMsaaboh8Bt7aylMPNqpGc3AlN2XvEUKhNZfvKDw84zS58sQvr5-L9dE23KpfDmPbO22vnzDqgxsF5YtL5dnlUeQDDZrWOL?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcAcdIsr3VuolKVsO4XpKcsdawZVSZHUEcTC5hY8MTyPIgWA5bK67DSnb7FIqMsaaboh8Bt7aylMPNqpGc3AlN2XvEUKhNZfvKDw84zS58sQvr5-L9dE23KpfDmPbO22vnzDqgxsF5YtL5dnlUeQDDZrWOL?key=amEUHfTdJnvQeZF3EjeoeA)

Para identificar los servicios que ofrece una máquina, podemos utilizar el escaneo de puertos con el argumento -sS que implementa esta técnica. Este método envía paquetes SYN a los puertos especificados y espera respuestas SYN-ACK de puertos abiertos, descartando los paquetes RST de puertos cerrados.

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXeFciKQyyBEPBzuz2SZpCsdy6ATxxhro3P0zeM0qpyysoibBHIngBre_xKwf50R8tWqNaYUZ428QFqZxD3tQYI6eMriQ1Ty8fAeXG5A3oZuyiAXS94owpNb5pZoT_cVJP_f2H3agAEhj_obfidFySszqUHN?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeFciKQyyBEPBzuz2SZpCsdy6ATxxhro3P0zeM0qpyysoibBHIngBre_xKwf50R8tWqNaYUZ428QFqZxD3tQYI6eMriQ1Ty8fAeXG5A3oZuyiAXS94owpNb5pZoT_cVJP_f2H3agAEhj_obfidFySszqUHN?key=amEUHfTdJnvQeZF3EjeoeA)

Como podemos ver, nmap muestra que el puerto 5432/tcp está abierto y asociado al servicio PostgreSQL. Esto confirma que el servicio está activo y escuchando en el puerto especificado, accesible desde la red.

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXcCPNpAz3vQz2ggp89uwWNgCBEJbf3zqad51Gv_O_a1smobPdNDLXdTXYrPfv51zOL_aKPzVA2JPjDm98BUMOGNdB0TFyF1qmo5B6--HaifeTVeeBF5Yc64ibJ75xABAJF31GKwDKDw2mPg3-NYQgYdeUyS?key=amEUHfTdJnvQeZF3EjeoeA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcCPNpAz3vQz2ggp89uwWNgCBEJbf3zqad51Gv_O_a1smobPdNDLXdTXYrPfv51zOL_aKPzVA2JPjDm98BUMOGNdB0TFyF1qmo5B6--HaifeTVeeBF5Yc64ibJ75xABAJF31GKwDKDw2mPg3-NYQgYdeUyS?key=amEUHfTdJnvQeZF3EjeoeA)

En la captura de Wireshark se observan los tres paquetes clave en el proceso de escaneo TCP SYN que realiza nmap:

- **Paquete SYN**:
    - **Source**: 192.168.122.1
    - **Destination**: 192.168.122.164 en el puerto 5432
    - Este es el primer paquete enviado desde la máquina de origen al puerto de destino. Es un paquete **SYN**, el cual indica el intento de iniciar una conexión TCP.
- **Paquete SYN-ACK**:
    - **Fuente**: 192.168.122.164
    - **Destino**: 192.168.122.1
    - En respuesta al paquete SYN, la máquina destino responde con un **SYN-ACK**, indicando que el puerto 5432 está **abierto** y escuchando conexiones. Este paquete confirma que el servicio PostgreSQL está accesible en ese puerto.
- **Paquete RST**:
    - **Fuente**: 192.168.122.1
    - **Destino**: 192.168.122.164
    - En lugar de completar la conexión enviando un ACK, nmap responde con un **RST** (Reset), lo cual indica que no desea establecer una conexión completa. Este paquete permite finalizar la "semi-conexión" sin necesidad de completar el protocolo de enlace de tres vías de TCP.

## 3. **Crea un honeypot a partir de una máquina Metasploitable 3 o similar. Toma el control del mismo aprovechando al menos dos vulnerabilidades diferentes. Realizad un video explicando el proceso.**

En primer lugar instalaremos metasploit framework en la maquina virtual atacante. [https://cerebrodigital.net/como-instalar-metasploit-framework-en-ubuntu-debian/](https://cerebrodigital.net/como-instalar-metasploit-framework-en-ubuntu-debian/)

Metasploit Framework es un proyecto de código abierto que proporciona la infraestructura, el contenido y las herramientas para realizar auditorías de seguridad y pruebas de penetración exhaustivas.

Primero descargamos el instalador de Metasploit ejecutando los siguientes comandos en su terminal:

```sql
curl [https://raw.githubusercontent.com/rapid7/metasploit-omnibus/master/config/templates/metasploit-framework-wrappers/msfupdate.erb](https://raw.githubusercontent.com/rapid7/metasploit-omnibus/master/config/templates/metasploit-framework-wrappers/msfupdate.erb) > msfinstall
```

Una vez descargado el script, lo hacemos ejecutable. → chmod 755 msfinstall y procedemos con su ejecución → ./msfinstall

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXe3YjEKO8kcDzbBd8Bczx6aN_s8AUTlCqsxiLvIkSpkg3uTo3vQkhDmxXxCCXImw7ez34mlppp9GxoyJ3Z9OkDo-4Q84R1OTcXaolFKqoIysVyVtDbHKdrD0tl7Ja9-DmGiQgWWi8r4uCyAAd-rluaM45Os?key=5XBjb5S6ZTJgQPnoKOipBA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXe3YjEKO8kcDzbBd8Bczx6aN_s8AUTlCqsxiLvIkSpkg3uTo3vQkhDmxXxCCXImw7ez34mlppp9GxoyJ3Z9OkDo-4Q84R1OTcXaolFKqoIysVyVtDbHKdrD0tl7Ja9-DmGiQgWWi8r4uCyAAd-rluaM45Os?key=5XBjb5S6ZTJgQPnoKOipBA)

Tras esto, procedemos a crear e inicializar la base de datos msf. → msfdb init

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXcYfwq4lqhgozQg12YNun0TCAHy_FBoai-bk0ToHiOtLvHtCSZzAtWMl-X2Gy3Z79lLkI6D3a8bvtdUoQGBH-nUQAwYhMZKaS8W8TQ7kIcc6_jKDmAJnGYGvXlQ36c29J5ypq0rbpQGpy2awBVzwetWStkW?key=5XBjb5S6ZTJgQPnoKOipBA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcYfwq4lqhgozQg12YNun0TCAHy_FBoai-bk0ToHiOtLvHtCSZzAtWMl-X2Gy3Z79lLkI6D3a8bvtdUoQGBH-nUQAwYhMZKaS8W8TQ7kIcc6_jKDmAJnGYGvXlQ36c29J5ypq0rbpQGpy2awBVzwetWStkW?key=5XBjb5S6ZTJgQPnoKOipBA)

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXcqJzB0SwA6DLBGxSa0MNGHGUsZ7ZbCFETvd1_8x7hVUYqbxvQz1BpsFEd8tYGn1OYTB2RLWAA8rLOtpuEZqYNZeBtokoDcWTtjoYHoz2u-wPUaIKBIJWcnT0pSLJSly699MrPJZfbD_uLHmpEep4MIQxA2?key=5XBjb5S6ZTJgQPnoKOipBA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcqJzB0SwA6DLBGxSa0MNGHGUsZ7ZbCFETvd1_8x7hVUYqbxvQz1BpsFEd8tYGn1OYTB2RLWAA8rLOtpuEZqYNZeBtokoDcWTtjoYHoz2u-wPUaIKBIJWcnT0pSLJSly699MrPJZfbD_uLHmpEep4MIQxA2?key=5XBjb5S6ZTJgQPnoKOipBA)

Ahora que la base de datos está inicializada, podemos iniciar **msfconsole** en nuestra maquina atacante.

A modo introductorio, aparte de la máquina atacante que tendrá instalado metasploit framework, tendré una máquina objetivo que en este caso es una maquina virtual metasploitable 2.6.2 la cual hemos instalado a partir del .ova que tenemos en [dit.gonzalonazareno.org](http://dit.gonzalonazareno.org) esta ova la hemos importado como servicio virtualizando en oracle virtual box, de forma que esta maquina con este SO será nuestra maquina objetivo durante la realización de este ejercicio.

**Explotación vulnerabilidad 1**

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXcHLEhbnJGA2HQq3pPLcKbmFvNsB0OkTmWICgJdPnnLsHkg8vUaATKFxS99S4dBwIgyaED_lMQhVANAfRyv1QWxYe2OTH5qQp_4bvq1lizoG8rRRIVBEIJFdOaKaBZRgYiflzZoXrzISakwnyvc69PLWw5E?key=5XBjb5S6ZTJgQPnoKOipBA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcHLEhbnJGA2HQq3pPLcKbmFvNsB0OkTmWICgJdPnnLsHkg8vUaATKFxS99S4dBwIgyaED_lMQhVANAfRyv1QWxYe2OTH5qQp_4bvq1lizoG8rRRIVBEIJFdOaKaBZRgYiflzZoXrzISakwnyvc69PLWw5E?key=5XBjb5S6ZTJgQPnoKOipBA)

La salida del escaneo muestra todos los puertos abiertos y los servicios que nmap ha identificado como corriendo en esos puertos.

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXc3uJEORFGS_Y4WMsEH0o6qBR-1xv952R5AXs5ff9PX0RE4GzNCV-b6S7b8l7jc916GiL9VVEmr4vaAgHGUkVfukGG_rjXfKjvI3nhE8i6q_UMTarAdQLZeaMfZbaISonG579aelja8HWB-FTZj3qUICUHu?key=5XBjb5S6ZTJgQPnoKOipBA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXc3uJEORFGS_Y4WMsEH0o6qBR-1xv952R5AXs5ff9PX0RE4GzNCV-b6S7b8l7jc916GiL9VVEmr4vaAgHGUkVfukGG_rjXfKjvI3nhE8i6q_UMTarAdQLZeaMfZbaISonG579aelja8HWB-FTZj3qUICUHu?key=5XBjb5S6ZTJgQPnoKOipBA)

Ejecutar msfconsole en la terminal lanza la consola principal de Metasploit, una potente herramienta de pruebas de penetración y explotación de vulnerabilidades. que hemos instalado antes.

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXe5OBwBKZRAsZxHkIlXTKv4pxmED3zJklDZtm0K3ndEtKFOGs903CH8mirCk3u7UDAJQZvvrfVFHnD5vlFKaXOB_FKWpFGP9aZORj15ySq79ubvfLSGBjlaHC45sQpDup5hQE1w0yM0CYrtotYDnjzkMROp?key=5XBjb5S6ZTJgQPnoKOipBA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXe5OBwBKZRAsZxHkIlXTKv4pxmED3zJklDZtm0K3ndEtKFOGs903CH8mirCk3u7UDAJQZvvrfVFHnD5vlFKaXOB_FKWpFGP9aZORj15ySq79ubvfLSGBjlaHC45sQpDup5hQE1w0yM0CYrtotYDnjzkMROp?key=5XBjb5S6ZTJgQPnoKOipBA)

**db_nmap**: Este comando permite ejecutar nmap directamente desde la consola de Metasploit, integrando los resultados del escaneo a la base de datos de Metasploit. Esto facilita la gestión de información sobre los objetivos y la planificación de ataques.

- **sV**: Es una opción de Nmap que sirve para hacer service version detection, es decir, intenta identificar la versión específica del servicio que está corriendo en un puerto abierto. Esto es útil porque, al conocer la versión, puedes saber si tiene vulnerabilidades conocidas.
- **192.168.1.134**: Es la dirección IP de la máquina objetivo que se va a escanear. En este caso, es la máquina Metasploitable2 que estás atacando.
- **-p 6667**: Esto indica que solo quieres escanear el puerto 6667, que es el puerto comúnmente utilizado para servicios IRC. El IRC (Internet Relay Chat) es un protocolo de comunicación en tiempo real, y en este caso, es donde corre el servicio UnrealIRCd en la máquina objetivo.

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXcV_63EB-2qJNx0O-FwmcRX2HzwUlYTSa0NZtOq0NmtaAtP0FUrTF_XPsZiqNhHhvi3mZbhYXscH8ys6c5qdRmEQWkzIldAIgpYBAJuFKL6znqPK3hco7vJI8PWYfdDfoYEuCx6Dq4XWHg2T3GVB3tVU_c?key=5XBjb5S6ZTJgQPnoKOipBA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcV_63EB-2qJNx0O-FwmcRX2HzwUlYTSa0NZtOq0NmtaAtP0FUrTF_XPsZiqNhHhvi3mZbhYXscH8ys6c5qdRmEQWkzIldAIgpYBAJuFKL6znqPK3hco7vJI8PWYfdDfoYEuCx6Dq4XWHg2T3GVB3tVU_c?key=5XBjb5S6ZTJgQPnoKOipBA)

Como sabemos que el puerto 6667 está abierto y tiene un servicio IRC corriendo en él, específicamente UnrealIRCd, que es un conocido software de servidor IRC, pues haremos una búsqueda de los exploits según el nombre de servicio indicado y nos muestra un resultado.

Hecho esto copiamos la ruta del exploit y para usarlo escribimos: 

```sql
use exploit/unix/irc/unreal_ircd_3281_backdoor
```

Un **exploit** es un software o un código diseñado para aprovechar una vulnerabilidad específica en un sistema, aplicación o servicio. La vulnerabilidad podría ser un fallo en el código, un error de configuración, o cualquier debilidad que permita que el exploit haga algo que el sistema normalmente no permitiría.

El exploit unreal_ircd_3281_backdoor que hemos utilizado en Metasploit fue diseñado específicamente para aprovechar una puerta trasera (backdoor) en una versión vulnerable de UnrealIRCd. El exploit se encarga de enviar un comando especial que le permite acceder a la máquina de forma no autorizada.

En resumen, el exploit es la herramienta para acceder a un sistema aprovechando una vulnerabilidad.

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXd_rwBNodulfrxOurh9FtxAY9W5WGqIJk5ARK3CjaLGXHmGkBtEsp7B3Qj6ejjAwOFDUr_uIL8QyU8cc3k1KNXwRiPnyBm3qGyZnw0SJFM8xupb-_80VW5Ok8ly1HZJ1T2HygcM1b_6mE7i0F7wreHwyko?key=5XBjb5S6ZTJgQPnoKOipBA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXd_rwBNodulfrxOurh9FtxAY9W5WGqIJk5ARK3CjaLGXHmGkBtEsp7B3Qj6ejjAwOFDUr_uIL8QyU8cc3k1KNXwRiPnyBm3qGyZnw0SJFM8xupb-_80VW5Ok8ly1HZJ1T2HygcM1b_6mE7i0F7wreHwyko?key=5XBjb5S6ZTJgQPnoKOipBA)

Definimos la IP de la máquina objetivo (192.168.1.134) como RHOST.

Tras esto cuando queremos ejecutar el exploit nos pide que necesitamos indicar un payload por lo que hacemos un shows payloads para ver cuales tenemos y en mi caso he seleccionado uno de los primeros → cmd/unix/bind_perl y lo cargo con set.

Un **payload** (o "carga útil") es el código que se ejecuta en el sistema objetivo una vez que el exploit ha tenido éxito. Es lo que realmente realiza la acción maliciosa o el comportamiento deseado por el atacante, como abrir una puerta trasera, iniciar una sesión de shell, o instalar un software.

Es decir, mientras que el exploit aprovecha la vulnerabilidad para entrar, el payload es lo que hace una vez dentro.

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXcQmgE_ZTg2wHoMxAXKywqrovE9em1XL1Cpu5XrPxBCRQjXPP6D7zVyWoqUK2GlOEsMhjSGYWe_WvwXWUklaYXPBg1nFBQ1ybSn3un4z7LCszUgs6yIXFgR3w2vRpcHln0fRHzSyoy0_VlWp1yVtno6YTQY?key=5XBjb5S6ZTJgQPnoKOipBA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcQmgE_ZTg2wHoMxAXKywqrovE9em1XL1Cpu5XrPxBCRQjXPP6D7zVyWoqUK2GlOEsMhjSGYWe_WvwXWUklaYXPBg1nFBQ1ybSn3un4z7LCszUgs6yIXFgR3w2vRpcHln0fRHzSyoy0_VlWp1yVtno6YTQY?key=5XBjb5S6ZTJgQPnoKOipBA)

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXfZ-fo-urrHQMolPufDdyy-qr9yH25u62CS5yPWkOJ7S6mc-pWX7n3Gxk0ZMfLPus_E3Ol7okHJf9uC2nlqypX2narWAqwJWUxEnCT6ZLw6nKM6GZft0oIhtivrcVmSaDlrIwWNLvR9pKIwKyY3V007csU?key=5XBjb5S6ZTJgQPnoKOipBA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfZ-fo-urrHQMolPufDdyy-qr9yH25u62CS5yPWkOJ7S6mc-pWX7n3Gxk0ZMfLPus_E3Ol7okHJf9uC2nlqypX2narWAqwJWUxEnCT6ZLw6nKM6GZft0oIhtivrcVmSaDlrIwWNLvR9pKIwKyY3V007csU?key=5XBjb5S6ZTJgQPnoKOipBA)

Ejecutamos de nuevo el exploit y bingo, podemos conectarnos con éxito a nuestra máquina objetivo esto lo hemos comprobado ejecutando comandos tipo: uname -a, hostname y ip a que nos identifican nuestra máquina objetivo.

Si ejecutamos los mismos comandos en la máquina metasploitable vemos que hablamos de la misma máquina y que hemos conseguido tomar el control sobre ella.

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXfFuHBrbHOUNeHuWAOUY2Lcx9kkm0eaWr3FVycLOXcUXcf0uds13FwZmnbm61MSlQvKr96YTw2Y6XrUMsDvoxIRDsWXFVa0cMAYhxHC4gr_T0EHeFOVJ1smaiM0-aFWi11TA7AwI4_tfuZnJqyJnGS8jzM2?key=5XBjb5S6ZTJgQPnoKOipBA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfFuHBrbHOUNeHuWAOUY2Lcx9kkm0eaWr3FVycLOXcUXcf0uds13FwZmnbm61MSlQvKr96YTw2Y6XrUMsDvoxIRDsWXFVa0cMAYhxHC4gr_T0EHeFOVJ1smaiM0-aFWi11TA7AwI4_tfuZnJqyJnGS8jzM2?key=5XBjb5S6ZTJgQPnoKOipBA)

**Explotación vulnerabilidad 2**

La salida del escaneo muestra todos los puertos abiertos y los servicios que Nmap ha identificado como activos en esos puertos. En este segundo caso de explotación de vulnerabilidades de nuestro honeypot, buscaremos explotar el puerto 21 (FTP), donde se está ejecutando el servicio vsftpd.

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXe6iD6flIocojOqwoNGfD8XX4zjYWwe3VPDo9QK45CkdAIFy_cMw27qQBYea0pm6E5yBDOSSSmBh8P-EtnOFVhke0jPdNwM7nMdm8zleasBtgaFU33acQ6eMLIyO2QD0nCXVUqUKCbE1YeAGJoM0wCHRh1u?key=5XBjb5S6ZTJgQPnoKOipBA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXe6iD6flIocojOqwoNGfD8XX4zjYWwe3VPDo9QK45CkdAIFy_cMw27qQBYea0pm6E5yBDOSSSmBh8P-EtnOFVhke0jPdNwM7nMdm8zleasBtgaFU33acQ6eMLIyO2QD0nCXVUqUKCbE1YeAGJoM0wCHRh1u?key=5XBjb5S6ZTJgQPnoKOipBA)

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXfsTKFOgSMcqysSpkX8ExsYU6uiLubcR1yL-n3aix1syHd1xccJoq0r_PUfwLTNPXRTNhRAHwHCMJOp4Ivur3h7tWcthp9S1-p5nF64CPYkkrhW4SzNTj8CHqBV--fmF34gZyKBvPGQeEIcaLP8j6FkeUD5?key=5XBjb5S6ZTJgQPnoKOipBA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfsTKFOgSMcqysSpkX8ExsYU6uiLubcR1yL-n3aix1syHd1xccJoq0r_PUfwLTNPXRTNhRAHwHCMJOp4Ivur3h7tWcthp9S1-p5nF64CPYkkrhW4SzNTj8CHqBV--fmF34gZyKBvPGQeEIcaLP8j6FkeUD5?key=5XBjb5S6ZTJgQPnoKOipBA)

A continuación al ejecutar **db_nmap -sV 192.168.1.134 -p 21**, se está realizando un escaneo Nmap en el puerto 21 del host 192.168.1.134, con el objetivo de identificar el servicio FTP que está corriendo en ese puerto y su versión.

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXdYXvbOZQrHAajhn7M_AiyaJ6b0GTcdVcxk0tX4TZBG3MpuAewysKB7P2It_KtDmLmAGrdEs-9gjJSBzPexSo6DSOe0tQl9tY2mx8-DQnp5u_0lEMd5p-B2FQLKDXDAOQdy4JeFFj-baUTfSZEqiuUTw0EZ?key=5XBjb5S6ZTJgQPnoKOipBA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdYXvbOZQrHAajhn7M_AiyaJ6b0GTcdVcxk0tX4TZBG3MpuAewysKB7P2It_KtDmLmAGrdEs-9gjJSBzPexSo6DSOe0tQl9tY2mx8-DQnp5u_0lEMd5p-B2FQLKDXDAOQdy4JeFFj-baUTfSZEqiuUTw0EZ?key=5XBjb5S6ZTJgQPnoKOipBA)

Buscamos los exploits correspondientes al servicio vsftpd, copiamos el rutas del exploit y la usamos con use, en este caso nos indica que tenemos un payload cargado por defecto.

Tras esto como vemos en la captura posterior, añadimos un valor con set a la variable RHOST que será la máquina objetivo, en este caso la ip de nuestra máquina metasploitable y ejecutamos el exploit y como vemos hemos conseguimos tomar el control de la máquina metasploitable.

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXdPTG7dd6x9j5Gge63MBw70T4lF8noVqrPvR9VZZJL3DCc4XAKd7melYn2vxYfRRHgzprMZI7n0j_Ksb990S-2CAiIIu7pCCagSZ54Uqju5aHBRnzjtzhHDkFZ771AcILFrnQ6oQWdAjQz8Vp5mpJbYTAM?key=5XBjb5S6ZTJgQPnoKOipBA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdPTG7dd6x9j5Gge63MBw70T4lF8noVqrPvR9VZZJL3DCc4XAKd7melYn2vxYfRRHgzprMZI7n0j_Ksb990S-2CAiIIu7pCCagSZ54Uqju5aHBRnzjtzhHDkFZ771AcILFrnQ6oQWdAjQz8Vp5mpJbYTAM?key=5XBjb5S6ZTJgQPnoKOipBA)

**Explotación vulnerabilidad 3**

Lo que vamos a hacer a continuación es como en los procesos anteriores que se describieron, pero esta vez vamos lo haremos dentro de la categoría escaner auxiliar (conocido también como auxiliary scanners), donde hemos seleccionado el módulo de samba, es cual es smb_version.

Este módulo en concreto lo vamos a usar para obtener la versión del protocolo **SMB (Server Message Block)** que está activo en el host el cual queremos atacar.

Por lo que en primer lugar entraremos en la consola de msfconsole:

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXcgfTyL7ynIYeep6PNqqSM0q1Qk9is66Ra0eHkqcPhogop1lXpcVoN4QYitPu_XOe71sqTF7X0NaRcm0rSAlAdJBvwB4McvMwWM3cR9F4ryK_tNd6MfPg7TyFNXFoYcTA1MvrW4JbWnWM4DHjgZPm-n9JPR?key=5XBjb5S6ZTJgQPnoKOipBA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcgfTyL7ynIYeep6PNqqSM0q1Qk9is66Ra0eHkqcPhogop1lXpcVoN4QYitPu_XOe71sqTF7X0NaRcm0rSAlAdJBvwB4McvMwWM3cR9F4ryK_tNd6MfPg7TyFNXFoYcTA1MvrW4JbWnWM4DHjgZPm-n9JPR?key=5XBjb5S6ZTJgQPnoKOipBA)

Lo primero que haremos será un escaneo de puertos para el hosts 192.168.1.161/24, para el cual usaremos el siguiente comando:

```powershell
db_nmap -sV 192.168.1.161
```

(Si nos dice que no encuentra nmap, deberás de meter el siguiente comando para su instalación: apt install nmap )

Desglose del comando:

- **db_nmap:** Este es un módulo integrado en Metasploit que proporciona funcionalidades de nmap.
- **sV**: Esta opción indica que se realizará un escaneo de versión (-sV).
- `192.168.1.161`: Es la dirección IP del objetivo que se quiere escanear.

Por lo que nos dará lo siguiente por pantalla:

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXebTdkUD3JCDIuAXWSJWICBps2R6LPw7SDOGtVEZXKSv3IG6VfF7daqs9q1NSZWo1UDO6-LSkZZIuly6gl4wX-B2D8xHgcVgdDqib2q7wJrHRe2W1s7BRNzLT7ShI6ErWOqgH1NnbxKGeL_RXGVkVepnL81?key=5XBjb5S6ZTJgQPnoKOipBA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXebTdkUD3JCDIuAXWSJWICBps2R6LPw7SDOGtVEZXKSv3IG6VfF7daqs9q1NSZWo1UDO6-LSkZZIuly6gl4wX-B2D8xHgcVgdDqib2q7wJrHRe2W1s7BRNzLT7ShI6ErWOqgH1NnbxKGeL_RXGVkVepnL81?key=5XBjb5S6ZTJgQPnoKOipBA)

Por lo que vemos los puertos y los servicios los cuales están corriendo, ahora lo que haremos será un escaneo más profundo al puerto del servicio samba , el cual es 445, por lo que el comando a meter será el siguiente:

```sql
db_nmap -sV -p 445 192.168.1.161
```

El cual nos muestra el puerto al que pertenece el servicio, su estado, el servicio al que pertenece, y su versión.

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXdO6KokC_YLAsp79evSrWejwUP5tpiLA_O70Za5k6NzXQIbXo4Hr7uTrPfYB1RR6kyITWxzoHxFJYF5L7_o_wm0hpreUeeoISZj_25AGcUuDyjk0dZeZ_vwHDsP6Xn6WFZDjNX7EmCs5Yn7ZLjfG5_Q5B1B?key=5XBjb5S6ZTJgQPnoKOipBA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdO6KokC_YLAsp79evSrWejwUP5tpiLA_O70Za5k6NzXQIbXo4Hr7uTrPfYB1RR6kyITWxzoHxFJYF5L7_o_wm0hpreUeeoISZj_25AGcUuDyjk0dZeZ_vwHDsP6Xn6WFZDjNX7EmCs5Yn7ZLjfG5_Q5B1B?key=5XBjb5S6ZTJgQPnoKOipBA)

Una vez hecho esto lo que haremos será usar el siguiente comando:

```powershell
use auxiliary/scanner/smb/smb_version
```

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXfmGnz5Z28IFF6pne0fUd8ZiUlwGaJqM6CAJUFMivtvJLFFTtEzF6Gk68F3ZL2bvD6PMclNfNve-sC8uMHG6FYSQ0Qwiv_oJbGMaB5jzEupx9-gcrGRGKV-Us0tR6jd9nTjYTLE-BTip5WH3mOQ-PoL-BiJ?key=5XBjb5S6ZTJgQPnoKOipBA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfmGnz5Z28IFF6pne0fUd8ZiUlwGaJqM6CAJUFMivtvJLFFTtEzF6Gk68F3ZL2bvD6PMclNfNve-sC8uMHG6FYSQ0Qwiv_oJbGMaB5jzEupx9-gcrGRGKV-Us0tR6jd9nTjYTLE-BTip5WH3mOQ-PoL-BiJ?key=5XBjb5S6ZTJgQPnoKOipBA)

y porque hacemos esto, pues esto lo estamos usando para escanear servidores SMB y saber que versión se está usando.

Por lo que si nos ponemos a traducir el comando, será lo siguiente:

- **auxiliary**: Significa que es un módulo extra, no un ataque directo.
- **scanner**: Es un tipo de módulo que se usa para hacer escaneos en redes.
- **smb**: Indica que se están escaneando servidores SMB.
- **smb_version**: Es el nombre del módulo que verifica la versión del servidor SMB.

Ahora tenemos que poner el destino al que queremos ver la vulnerabilidad, es decir la dirección IP, Junto con su puerto, el cual son los siguiente comandos:

```powershell
set RHOST 192.168.1.161
```

```powershell
set RPORT 445
```

Una vez que tenemos esto, si metemos el comando show options, nos deberá de aparecer lo siguiente:

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXeYZX6tNtEnzcvE1hs7nd7Q8GH-n4a5rJIdYZlODf0wawwLuis3zjp9v4IeNFURokTjJAq09Av5Co1M3NSY4q6Es6en5wtRQD6z4uTfYCH3pKRsrM2pqeyo9z2Wp9t7DW64OenpMg-C7G0DMeiuJkk6rkWT?key=5XBjb5S6ZTJgQPnoKOipBA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeYZX6tNtEnzcvE1hs7nd7Q8GH-n4a5rJIdYZlODf0wawwLuis3zjp9v4IeNFURokTjJAq09Av5Co1M3NSY4q6Es6en5wtRQD6z4uTfYCH3pKRsrM2pqeyo9z2Wp9t7DW64OenpMg-C7G0DMeiuJkk6rkWT?key=5XBjb5S6ZTJgQPnoKOipBA)

Para ver las vulnerabilidades usaremos la herramienta open source, la cual para atacar smb, nos dice que la más vulnerable se corresponde con el siguiente codigo: ****EXPLICAR COMO CONSEGUIR EL CODIGO**

```powershell
cve:2007-2447
```

El cual en nuestra consola tendremos que buscar el código de la siguiente manera:

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXcVvjaL_bnltpLdLisk7pV1YfE5A1n7wXDw0HNv6pxP_d5CWNTDkKmJap0XPg3Fk_VTG3XRMuggHrZ3oOVhm5ZycwOxTs8wofxiLqleLwtxHFvaJnCWlDVlHiN7jkRzxzlnfltg8B8Du0ONM0u4VAtKMxbA?key=5XBjb5S6ZTJgQPnoKOipBA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcVvjaL_bnltpLdLisk7pV1YfE5A1n7wXDw0HNv6pxP_d5CWNTDkKmJap0XPg3Fk_VTG3XRMuggHrZ3oOVhm5ZycwOxTs8wofxiLqleLwtxHFvaJnCWlDVlHiN7jkRzxzlnfltg8B8Du0ONM0u4VAtKMxbA?key=5XBjb5S6ZTJgQPnoKOipBA)

Y como vemos por pantalla en la ultima linea, nos esta diciendo que esta vulnerabilidad que hemos encontrado pertenece a este exploit, por lo que haremos será copiar esa linea y ponerlo en la consola:

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXemKfXK66BOveapHlet8DyE4_Q5hXlayiAm9-7Jxb8j34BJpHS5aC6V3vSkrRi_Sys-TYTxCQGHggOLdJRJEWdLmCI9pj_bEk8c4NjJ7rjhFSfVucZgi4L4kfFBl4x3jsIbPevcs0aL0U6OBk8hNfh9hc8?key=5XBjb5S6ZTJgQPnoKOipBA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXemKfXK66BOveapHlet8DyE4_Q5hXlayiAm9-7Jxb8j34BJpHS5aC6V3vSkrRi_Sys-TYTxCQGHggOLdJRJEWdLmCI9pj_bEk8c4NjJ7rjhFSfVucZgi4L4kfFBl4x3jsIbPevcs0aL0U6OBk8hNfh9hc8?key=5XBjb5S6ZTJgQPnoKOipBA)

Ahora volvemos a meter el comando show options, para ver si falta algún dato:

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXd-2bhyvev4yYV4zIOa4tdYVYtzwwArL41TvK_0dvSd22Bf8xEs2z2Pp-Cs7NEoXF4ObsCZzc9yfZipD9FoR5tQy3Wr-zqv7zVfIKTt8FlHrFFnc2Nnay_Hk2UBXvyN15KhYBgY2mkLVejhcD4R9t3SiaQB?key=5XBjb5S6ZTJgQPnoKOipBA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXd-2bhyvev4yYV4zIOa4tdYVYtzwwArL41TvK_0dvSd22Bf8xEs2z2Pp-Cs7NEoXF4ObsCZzc9yfZipD9FoR5tQy3Wr-zqv7zVfIKTt8FlHrFFnc2Nnay_Hk2UBXvyN15KhYBgY2mkLVejhcD4R9t3SiaQB?key=5XBjb5S6ZTJgQPnoKOipBA)

Como vemos nos falta la ip y su puerto de destino, por lo que la tendremos que meter:

```powershell
set RHOSTS 192.168.1.161
```

```powershell
set RPORT 445
```

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXd5pFLB5GAO7KwtJLDe0A5gqj7s-79uBo8nCjyf8rXfNSLpxTHsiejrS6fTGeCJYk4cpfyDTjZNqRBGm4BtbPiGPtGYbW8ZtEh9W35OGDZQNqFumXflKaY7pRRD-UHfZTiC4t7HrflvKKCDE6nghyabXlKj?key=5XBjb5S6ZTJgQPnoKOipBA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXd5pFLB5GAO7KwtJLDe0A5gqj7s-79uBo8nCjyf8rXfNSLpxTHsiejrS6fTGeCJYk4cpfyDTjZNqRBGm4BtbPiGPtGYbW8ZtEh9W35OGDZQNqFumXflKaY7pRRD-UHfZTiC4t7HrflvKKCDE6nghyabXlKj?key=5XBjb5S6ZTJgQPnoKOipBA)

Ahora que tenemos esto, buscaremos el payload que vamos a usar, por lo que veremos las distintas opciones que tenemos con show payload:

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXcePA_Cpg0_qJQ-ggOP3N1Ph1msik7k7FFpNlzqvl7Pv5EjfVTPevq-E2QSkX0Xmb3hjfRpAt5jbPmTaNdfYishb-m3Rc8h5GHw4qnfeApIsHhhVUS9qheKWbNOaKVRSIZ7RouFylOijj7eR6R0mfba7pl-?key=5XBjb5S6ZTJgQPnoKOipBA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcePA_Cpg0_qJQ-ggOP3N1Ph1msik7k7FFpNlzqvl7Pv5EjfVTPevq-E2QSkX0Xmb3hjfRpAt5jbPmTaNdfYishb-m3Rc8h5GHw4qnfeApIsHhhVUS9qheKWbNOaKVRSIZ7RouFylOijj7eR6R0mfba7pl-?key=5XBjb5S6ZTJgQPnoKOipBA)

De toda esta lista usaremos la numero 20, el cual la hemos elegido, por el tipo de exploit que estamos haciendo, la compatibilidad con el S.O. el tipo de acceso, la conexión, y su funcionalidad.

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXcqdp_bQaxe-50wto1GERgaikFEKtBnjlz79LtdJNAL8CvMeAu-Y_BCPNpdfOxiNO9GJbk2FIhJEYXlEu-i2NAjgwrRgErm9Y8oeygC98T4Ku70ZbJ5YAmIbKmwJScYX6io0UaEG7Y-DLXID6ywrPLaY7Tk?key=5XBjb5S6ZTJgQPnoKOipBA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcqdp_bQaxe-50wto1GERgaikFEKtBnjlz79LtdJNAL8CvMeAu-Y_BCPNpdfOxiNO9GJbk2FIhJEYXlEu-i2NAjgwrRgErm9Y8oeygC98T4Ku70ZbJ5YAmIbKmwJScYX6io0UaEG7Y-DLXID6ywrPLaY7Tk?key=5XBjb5S6ZTJgQPnoKOipBA)

Y ya que tenemos todo esto, con todos los ajustes hecho, lo que tendremos que hacer es ejecutar el exploit, de la siguiente manera:

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXdR0XOrVzwv9kbsrAMzHhAGvnUGK4wsYa3vNGH3VHSvfPUfPWbe_SG3FY6aRRWl14oBSltZhwaaY9ePafmnzJaKIhx6_58gsA62FWb-udwXdSckjmJK2TJQwelzUk2XB_tkVxW3yD9rXj0CSa04T3X3kyM?key=5XBjb5S6ZTJgQPnoKOipBA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdR0XOrVzwv9kbsrAMzHhAGvnUGK4wsYa3vNGH3VHSvfPUfPWbe_SG3FY6aRRWl14oBSltZhwaaY9ePafmnzJaKIhx6_58gsA62FWb-udwXdSckjmJK2TJQwelzUk2XB_tkVxW3yD9rXj0CSa04T3X3kyM?key=5XBjb5S6ZTJgQPnoKOipBA)

Y una vez que vemos esto por pantalla ya estaríamos dentro de la terminal del objetivo, y para comprobarlo haré un uname -a

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXeiv4G3hivwxFIOH4kI7SAfsWFcCt3vUvqp_ScRJQODoJQKTaqwvCC-IvfsEOTolddqmq_dL5FN6jX1IObAnosvtki4dXG9gOB7nVJxFvXvTFx2NGSd9aIQ949YlHsrmrkenqZ6JEwwDCavNWuwWPvIgQIc?key=5XBjb5S6ZTJgQPnoKOipBA](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeiv4G3hivwxFIOH4kI7SAfsWFcCt3vUvqp_ScRJQODoJQKTaqwvCC-IvfsEOTolddqmq_dL5FN6jX1IObAnosvtki4dXG9gOB7nVJxFvXvTFx2NGSd9aIQ949YlHsrmrkenqZ6JEwwDCavNWuwWPvIgQIc?key=5XBjb5S6ZTJgQPnoKOipBA)

## 4. Explicad en formato de artículo técnico para un blog o en un vídeo la diferencia entre vulnerabilidad, exploit y payload.

Cuando hablamos de ciberseguridad, es muy común oír hablar de los términos vulnerabilidad, exploit y payload. A continuación, explicaremos cada uno de ellos, sus diferencias, y cómo se relacionan entre sí.

### ***Vulnerabilidad***

Una vulnerabilidad es una **debilidad** en un sistema, aplicación o red que podría ser explotada por un atacante para realizar actividades malintencionadas. Las vulnerabilidades pueden surgir debido a errores en el código, malas configuraciones, o problemas de diseño. Una vez que se identifica una vulnerabilidad, el equipo de seguridad puede intentar solucionarla, pero si queda sin corregir, los atacantes pueden aprovecharla.

- Ejemplo de vulnerabilidad: Una **mala configuración en un servidor web** que permita acceder a los datos de la web. También puede ser una **mala gestión en las contraseñas**, o una mala configuración en algún servicio.

Hay muchas vulnerabilidades y muchos métodos para detectarlas, dos de los más comunes son **OpenVAS** o **Nessus.**

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXcuDFiy24JWmR3LIwE_dlnrnhO2Hd4C4pZZsNTYSpp_ospHf_QmasuAkMUiThRDaOMCyRSI7Bvf0gzrKjogX8a1BIPVMjjodsigKgxqOiwgKFubu6GeEP3qbNuIwqPcuZSCLnEvmEQawOsMAc6g7r8LQ_oH?key=-PlmlnvQ1CukgYene0Msioch](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcuDFiy24JWmR3LIwE_dlnrnhO2Hd4C4pZZsNTYSpp_ospHf_QmasuAkMUiThRDaOMCyRSI7Bvf0gzrKjogX8a1BIPVMjjodsigKgxqOiwgKFubu6GeEP3qbNuIwqPcuZSCLnEvmEQawOsMAc6g7r8LQ_oH?key=-PlmlnvQ1CukgYene0Msioch)

Se pueden observar muchos ejemplos de vulnerabilidad y también observamos los distintos tipos que hay de las mismas, críticas son las vulnerabilidades más peligrosas para el usuario porque son las que más provecho podemos sacar atacándolas, conforme van bajando el tipo de vulnerabilidad menos peligrosas son pero pueden seguir siendo aprovechadas.

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXfcAk-qVZzA9ipNrbNWrGw8VDt5KrTHygLUmichfWz3pgQlMlFqa1chmABbXHCb90RAHiswH5najpTEDe9i0EuJH511RypTBTYLzZNO6xVDh7kxb5Qg_wepriHmdNr_dS5F_eWg_BfVABk0Sywhpz1ORDez?key=-PlmlnvQ1CukgYene0Msioch](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfcAk-qVZzA9ipNrbNWrGw8VDt5KrTHygLUmichfWz3pgQlMlFqa1chmABbXHCb90RAHiswH5najpTEDe9i0EuJH511RypTBTYLzZNO6xVDh7kxb5Qg_wepriHmdNr_dS5F_eWg_BfVABk0Sywhpz1ORDez?key=-PlmlnvQ1CukgYene0Msioch)

Cada vulnerabilidad tiene su descripción y las más comunes tienen como solucionarlas ya sea por una actualización o mediante la instalación de otra cosa.

### ***Exploit***

Un **exploit** es una técnica o código que aprovecha una vulnerabilidad específica en un sistema para lograr objetivos como el acceso no autorizado o la ejecución de código malicioso. Actúa como un "puente" entre la vulnerabilidad y el atacante, aprovechando la debilidad del sistema o red para manipularlo de una manera no permitida

Para **buscar un exploit**, un atacante comienza identificando las vulnerabilidades del objetivo mediante herramientas de escaneo como **Nmap** o **Nessus**. Posteriormente, recurre a bases de datos públicas de exploits, como **Exploit-DB** o **GitHub**, donde puede filtrar por nombre de software, versión o tipo de vulnerabilidad.

Si la vulnerabilidad está registrada con un **CVE** (Common Vulnerabilities and Exposures), el atacante puede consultar detalles y exploits asociados en plataformas como **CVE Details**. Además, muchos hackers emplean frameworks como **Metasploit**, que no solo agiliza la búsqueda de exploits preconfigurados, sino que también permite ejecutar ataques con payloads predefinidos en solo minutos.

**Ejemplo de exploit**: un programa diseñado para aprovechar la vulnerabilidad **CVE-2024-6387**, que afecta el protocolo **SSH**. Esta vulnerabilidad podría identificarse inicialmente con un escáner y, posteriormente, buscarse el exploit correspondiente en **GitHub** o en otros sitios similares.

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXf-c_oCvBFNhEJGBfOvWRczs52Sqi8ucFC6oKEbDYzq3Sh345FpZ8DKFdNMuypFGfE-K7TshLFM3DdB1HcoZEp1sUs8LEhBwoCZxItH-cljxFST0dwDhcbzO_EBHB4FSNYFuuOt3Jz-5_WqjEKzfGHqzRc-?key=-PlmlnvQ1CukgYene0Msioch](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf-c_oCvBFNhEJGBfOvWRczs52Sqi8ucFC6oKEbDYzq3Sh345FpZ8DKFdNMuypFGfE-K7TshLFM3DdB1HcoZEp1sUs8LEhBwoCZxItH-cljxFST0dwDhcbzO_EBHB4FSNYFuuOt3Jz-5_WqjEKzfGHqzRc-?key=-PlmlnvQ1CukgYene0Msioch)

(Esto es una parte del exploit para saber cómo se vería)

### ***Payload***

El payload es el "código" que un atacante envía y ejecuta en el sistema después de que el exploit haya tenido éxito. Los payloads pueden tener distintas funciones, desde mostrar un mensaje hasta instalar malware o abrir una puerta trasera en el sistema. Su función principal es ejecutar las instrucciones que el atacante desee.

- Ejemplo de payload: Hay varios tipos de payloads dependiendo lo que queramos.

- ***Reverse Shell (Shell Inversa)***

Un reverse shell permite que el sistema víctima se conecte de vuelta al sistema del atacante, abriendo una línea de comandos remota. Esto es útil para los atacantes porque, en lugar de tener que abrir un puerto en el sistema objetivo, simplemente esperan una conexión de la víctima.

- Ejemplo: linux/x86/meterpreter/reverse_tcp en Metasploit. Este payload abre una conexión de shell inversa en un sistema Linux, permitiendo al atacante ejecutar comandos.
- ***Bind Shell***

Un bind shell es un payload que abre una línea de comandos en el sistema objetivo y escucha en un puerto específico, esperando a que el atacante se conecte. A diferencia del reverse shell, aquí el sistema objetivo escucha activamente, y el atacante se conecta cuando está listo.

- Ejemplo: windows/x64/meterpreter/bind_tcp en Metasploit, que permite al atacante conectarse a la máquina víctima y ejecutar comandos en ella.
- ***Meterpreter***

Meterpreter es un payload avanzado de Metasploit que proporciona una línea de comandos interactiva con funcionalidades avanzadas. Permite ejecutar comandos, gestionar archivos, tomar capturas de pantalla, grabar audio, y realizar otras acciones en el sistema objetivo.

- Ejemplo: windows/meterpreter/reverse_tcp o linux/x64/meterpreter_reverse_http, que permiten ejecutar una sesión de Meterpreter en el sistema objetivo y obtener control avanzado.
- ***Keylogger***

Un keylogger es un payload que captura y registra todas las pulsaciones de teclas en el sistema objetivo, lo que permite al atacante obtener información sensible, como contraseñas o mensajes.

- Ejemplo: Un script de Python o un módulo de Meterpreter que habilita el registro de teclas en el sistema comprometido.

### ***Relación entre vulnerabilidad, exploit y payload***

Una **vulnerabilidad** es una debilidad en el sistema que puede originarse por errores de código, configuraciones incorrectas o problemas de diseño. Si esta vulnerabilidad no se corrige, un atacante puede aprovecharla mediante un **exploit**: el código o técnica que explota esa debilidad para llevar a cabo un ataque malicioso, como obtener acceso no autorizado o ejecutar código en el sistema objetivo.

Una vez que el exploit tiene éxito, se ejecuta el **payload**, que contiene las instrucciones finales que el atacante desea ejecutar, como abrir una conexión remota o instalar malware en el sistema.

En resumen, la vulnerabilidad representa la oportunidad para un ataque, el exploit aprovecha esa oportunidad, y el payload ejecuta las acciones que completan el ataque.

## 5. Uso de Shodan.

### **GHDB (Google Hacking Database) es una herramienta muy útil para averiguar cómo localizar con Shodan un tipo de dispositivo concreto. Explicar qué son los dorks y emplear GHDB para averiguar cómo localizar cámaras IP que tengan una IP pública con Shodan. ¿Es un producto de Google? ¿Por qué se llama así?. Una vez localizada, entregad una captura de pantalla donde se vea la localización de la cámara, el país, el proveedor de internet, los puertos abiertos.**

Para este ejercicio usaremos GHDB. **Google Hacking Database (GHDB)** es una colección de "dorks" o consultas avanzadas para realizar búsquedas en Google con el objetivo de buscar una información determinada o posible información sensible expuesta en la web, es decir, Google Hacking Database otorga filtros avanzados de google para que podamos buscar lo que queramos en dicho navegador, como webcams, información, etc.

A estos filtros avanzados se les denominan **Dorks** y son ****una combinación específica de operadores y palabras clave que se usan para filtrar resultados de manera precisa para encontrar lo que queramos. Por ejemplo, se pueden usar operadores como intitle: (Busca una palabra en el título de la página), inurl: (Busca una palabra en la URL), filetype: (Busca un tipo de archivo específico como pdf, doc, img).

Google Hacking Database no es un producto de google pero se denomina así porque usa dicho motor de búsqueda para filtrar los resultados con sus dorks. GHDB lo creó Johnny Long en 2000 y ahora lo mantiene Offensive Security.

Vamos a ver cómo funciona y cómo podemos localizar una webcam y mirar su información en Shodan, para ello lo primero que debemos hacer es entrar en GHDB con el siguiente enlace: [https://www.exploit-db.com/google-hacking-database](https://www.exploit-db.com/google-hacking-database)

Una vez estamos en este enlace vamos a buscar una palabra clave, en nuestro caso será cam porque queremos acceder a una webcam.

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXdj5kg4uvyIIj3_nnVoqjL01heys0iRrTtxaYXIJpS389DIoYLySylu21u1JlZRjoL_yBVvEKXjMHk0oY8RwnGGsUZfnjER-HGHVS_TN-uf90qesple6Qv5B_g8CvVFZJTNqfW_TrO80B3AbJrPehbDPGdQ?key=MAIFLMIIlDk8uFPvMQhNJw](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdj5kg4uvyIIj3_nnVoqjL01heys0iRrTtxaYXIJpS389DIoYLySylu21u1JlZRjoL_yBVvEKXjMHk0oY8RwnGGsUZfnjER-HGHVS_TN-uf90qesple6Qv5B_g8CvVFZJTNqfW_TrO80B3AbJrPehbDPGdQ?key=MAIFLMIIlDk8uFPvMQhNJw)

Como observamos al introducir la palabra clave ‘cam’ nos aparecen muchos Dorks para buscar webcams, vamos a probar con el primero de ellos, para ello haremos click en el enlace del Dork que queramos, que en mi caso será **intitle:"Network Camera" inurl:main.cgi**

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXcFCXc8Eeg0rtdM3Y1W5PLgB7ETS7H1CX5QgUxb2bRRWOc7OfI6bFpDYnmj4XQLfY_-asAJRtYlnXEu_zSY3AJ0owGnylUsUZWlGOkOtSowIopSeova0XfXZriwzHGn60n_TjlSnZzrN98U94Kq?key=MAIFLMIIlDk8uFPvMQhNJw](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcFCXc8Eeg0rtdM3Y1W5PLgB7ETS7H1CX5QgUxb2bRRWOc7OfI6bFpDYnmj4XQLfY_-asAJRtYlnXEu_zSY3AJ0owGnylUsUZWlGOkOtSowIopSeova0XfXZriwzHGn60n_TjlSnZzrN98U94Kq?key=MAIFLMIIlDk8uFPvMQhNJw)

Una vez clickemos donde queramos nos mostrará el ID del Dork en el GHDB, su autor (S THAKUR), la fecha en la que fue publicado y en el texto de abajo nos muestra un poco más de información como la categoría a la que pertenece dicho Dork (Various Online Devices).

Pero lo importante es lo que he señalado, el Dork que nos mostrará la información que buscamos, una vez clickemos en ese Dork nos llevará a Google y hará un filtro para mostrar las Webcams.

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXcM1tuobVowmWhqucm49b5JIOUi75lww2WMbnx_bCGZbConWkClY4j9RwFUecNXAZ_bjT6rJxmPvIgrj1IJxg1tiJZowsUCGCu8-hLOnlwDMx8m4R2hsD6MYEJsaYulAmyWN5rUiuZedun5fGu2X_1fBQw?key=MAIFLMIIlDk8uFPvMQhNJw](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcM1tuobVowmWhqucm49b5JIOUi75lww2WMbnx_bCGZbConWkClY4j9RwFUecNXAZ_bjT6rJxmPvIgrj1IJxg1tiJZowsUCGCu8-hLOnlwDMx8m4R2hsD6MYEJsaYulAmyWN5rUiuZedun5fGu2X_1fBQw?key=MAIFLMIIlDk8uFPvMQhNJw)

Ya tenemos el Dork hecho y el resultado de la búsqueda, para encontrar información de estas Webcams en Shodan lo que haremos será copiar la dirección IP que aparece en el enlace que queramos y la introduciremos en el buscador de Shodan.

En mi caso para este ejemplo usaré la IP de la webcam ‘185.149.19.52’.

La introducimos en el buscador de Shodan ([https://www.shodan.io/](https://www.shodan.io/))

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXe-Hn5hqkoSiIrEFR-6bMAb6muiFubSLTQQ4RRCIA9Hqxc-vu5wHgVyIHB-qB6WXaFyqpxGGQnLZcwf3HU9VJwZ8CBo1k24GLbke244dhWJD0X4y0o1kcAG8Wf_1Urm_oat76S-0VWeyHlLrKiImQ6at71_?key=MAIFLMIIlDk8uFPvMQhNJw](https://lh7-rt.googleusercontent.com/docsz/AD_4nXe-Hn5hqkoSiIrEFR-6bMAb6muiFubSLTQQ4RRCIA9Hqxc-vu5wHgVyIHB-qB6WXaFyqpxGGQnLZcwf3HU9VJwZ8CBo1k24GLbke244dhWJD0X4y0o1kcAG8Wf_1Urm_oat76S-0VWeyHlLrKiImQ6at71_?key=MAIFLMIIlDk8uFPvMQhNJw)

Una vez hecho esto ya podremos ver el país de la webcam (Noruega), la ciudad de la webcam (Hovden), el proveedor de internet (Telefiber AS), los puertos abiertos (1024) y podemos acceder a la webcam.

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXcsTEUmdDh3ejQaMieBDM2qQLdiROaPN_E7all1cz-rnIGiAi6P8NOFkjtaUD9WRCA_FOR_JDSYDxXSVu5T-cl5qJfX74pcP1JP1D-YbWDn8aSKwZ4JYhtTKRBKglVM0Fzjhv472r8quXtnTHl6LgzHDlVs?key=MAIFLMIIlDk8uFPvMQhNJw](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcsTEUmdDh3ejQaMieBDM2qQLdiROaPN_E7all1cz-rnIGiAi6P8NOFkjtaUD9WRCA_FOR_JDSYDxXSVu5T-cl5qJfX74pcP1JP1D-YbWDn8aSKwZ4JYhtTKRBKglVM0Fzjhv472r8quXtnTHl6LgzHDlVs?key=MAIFLMIIlDk8uFPvMQhNJw)

Así se usa **GHDB** para encontrar información de una Webcam con IP pública en Shodan.

### **Comprobad si hay algún sistema con “Windows XP” conectado a internet, ¿en qué país?, ¿qué puerto está exponiendo?. Razona tu respuesta: ¿qué problemas de seguridad puede tener?,¿por qué crees que puede exponerse a ataques una máquina tan vulnerable?**

Para comprobar si hay sistemas con Windows XP conectados a Internet usando Shodan, podríamos realizar una búsqueda con el siguiente filtro:

```powershell
os:"Windows XP"
```

[https://lh7-rt.googleusercontent.com/docsz/AD_4nXfw3QYKkgqR2p81qxj8BQ3Z5zmqhVh48LttBfBIJJOhLwncottwmC_TtgypofmU8htoUnls58GuYDlaU0ztxrI6o5GMD-kgBD7xg0rChEDM3ZClTz5HqBGFcs5JU0J_oH2ytwQdBaw-Y-_yjTVDsqqFDkM?key=MAIFLMIIlDk8uFPvMQhNJw](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfw3QYKkgqR2p81qxj8BQ3Z5zmqhVh48LttBfBIJJOhLwncottwmC_TtgypofmU8htoUnls58GuYDlaU0ztxrI6o5GMD-kgBD7xg0rChEDM3ZClTz5HqBGFcs5JU0J_oH2ytwQdBaw-Y-_yjTVDsqqFDkM?key=MAIFLMIIlDk8uFPvMQhNJw)

Basándome en los resultados de la búsqueda en Shodan, podemos extraer la siguiente información sobre sistemas Windows XP conectados a Internet:

**Ubicación de los dispositivos Windows XP conectados a Internet**

- **Cantidad total de dispositivos:** 4,851
- **Principales países:**
    - **Corea del Sur:** 2,653 dispositivos
    - **China:** 824 dispositivos
    - **Países Bajos:** 448 dispositivos

Esta distribución geográfica puede indicar que en ciertos países se siguen utilizando sistemas Windows XP debido a limitaciones presupuestarias, dependencias de aplicaciones específicas que solo funcionan en este sistema o menor regulación sobre seguridad de TI. Corea del Sur y China, especialmente, parecen tener una mayor presencia de estos dispositivos.

**Puertos más utilizados**

- **Puerto 23 (Telnet):** Utilizado por 2,549 dispositivos. Este protocolo permite acceso remoto, pero carece de cualquier cifrado, lo cual expone los datos transmitidos (como contraseñas) a posibles intercepciones. La existencia de este puerto en sistemas sin soporte como Windows XP es una grave vulnerabilidad, ya que estos dispositivos podrían ser fácilmente comprometidos y controlados de forma remota.
- **Puerto 1433 (SQL Server):** Utilizado por 1,916 dispositivos. Este puerto se utiliza para conexiones a Microsoft SQL Server. Tenerlo expuesto en un sistema tan desactualizado aumenta la probabilidad de que atacantes puedan acceder a la base de datos, lo que podría incluir información sensible o confidencial sin medidas de protección actualizadas. Los ataques como la inyección SQL son amenazas significativas cuando el sistema no está adecuadamente asegurado.
- **Puerto 465 (SMTPS):** Utilizado por 25 dispositivos**.** Utilizado para comunicaciones seguras mediante SMTPS (Simple Mail Transfer Protocol Secure). Aunque este puerto suele ser más seguro, en un sistema sin soporte podría no estar correctamente configurado o utilizar cifrado obsoleto, lo que podría exponer datos importantes o permitir ataques de interceptación.

**Problemas de seguridad de Windows XP**

Windows XP fue lanzado en 2001 y alcanzó el final de su vida útil el 8 de abril de 2014. Desde entonces, Microsoft dejó de ofrecer parches y actualizaciones de seguridad, lo cual significa que cualquier vulnerabilidad encontrada en el sistema desde esa fecha permanece sin corregir. Esto implica los siguientes riesgos:

- **Vulnerabilidades conocidas sin parchear:** Las vulnerabilidades encontradas después de 2014 son públicas y pueden ser explotadas sin dificultad, ya que no existe soporte de seguridad para Windows XP.
- **Compatibilidad limitada con software moderno:** Esto hace que, si los sistemas deben utilizar software actual, pueden enfrentar problemas de incompatibilidad y, en muchos casos, ejecutar versiones desactualizadas de software, que también presentan vulnerabilidades.
- **Deficiencia en protocolos de seguridad modernos:** Windows XP carece de soporte para muchos de los protocolos de seguridad modernos y sus versiones de herramientas como el navegador o el servidor de base de datos están desactualizadas, aumentando su vulnerabilidad ante amenazas comunes como el ransomware.

**Causas de exposición a ataques de una máquina tan vulnerable**

Exponer un sistema como Windows XP en Internet es un riesgo elevado, y puede ocurrir por varias razones:

- **Dependencia de aplicaciones específicas:** Algunos sistemas críticos en entornos industriales, médicos o gubernamentales dependen de aplicaciones diseñadas solo para Windows XP. La actualización a un sistema moderno requeriría migrar o rediseñar estas aplicaciones, lo cual es costoso y a veces no es una opción.
- **Falta de presupuesto o recursos técnicos:** En algunos casos, las organizaciones no cuentan con los recursos financieros para actualizar o reemplazar los sistemas antiguos, especialmente en regiones o sectores con menor acceso a fondos tecnológicos.
- **Configuración incorrecta:** Es posible que estos sistemas se hayan configurado incorrectamente o con una seguridad mínima, especialmente si las redes en las que se encuentran están mal gestionadas.

### Localizad un servidor de Minecraft vulnerable a CVE-2021-44228. Explica cómo se parchea esta vulnerabilidad. Opcional: Graba un vídeo demostrando cómo podrías atacar un servidor vulnerable a CVE-2021-44228. Recuerda que debe ser un servidor propio para no tener problemas legales.

kdsjffsdf