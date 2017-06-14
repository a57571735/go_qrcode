# go_qrcode
golang 编码,解码二维码 ，感谢 bieber的帮助  
解码需要#include <zbar.h> c语言库的支持

开始要 go get github.com/happyEgg/go_qrcode  

引入第三方库 go get github.com/boombuler/barcode  

例子  
package main  

import (  
	"fmt"  
	"image/png"  
	"os"  

	qrcode "github.com/happyEgg/go_qrcode"
)

func main() {  

	img := qrcode.Encode("test qrcode", 300, 300)

	file, err := os.Create("./test.png")
	if err != nil {  
		fmt.Println(err)  
		return  
	}

	defer file.Close()  

	err = png.Encode(file, img)  
	if err != nil {  
		fmt.Println(err)  
		return  
	}

	value := qrcode.Decode("./test.png")  
	fmt.Println(value)
}

# 如何安装zbar
sudo yum -y install epel-release pygtk2.x86_64 zbar-pygtk.x86_64 pygtk2-devel.x86_64 pygtk2-doc.noarch pygobject2.x86_64 pygobject2-devel.x86_64 pygobject2-doc.x86_64  gtk2 gtk2-devel gtk2-devel-docs pdftk ImageMagick ImageMagick-devel ghostscript Python-imaging python-devel python-gtk2-dev libqt4-dev PyQt4.x86_64 PyQt4-devel.x86_64

wget http://ftp.gnome.org/pub/GNOME/sources/pygtk/2.24/pygtk-2.24.0.tar.gz

tar -zvxf pygtk-2.24.0.tar.gz

cd pygtk-2.24.0

./configure

make  

sudo make install  

wget http://downloads.sourceforge.net/project/zbar/zbar/0.10/zbar-0.10.tar.gz  

tar -zvxf zbar-0.10.tar.gz  

cd zbar-0.10

./configure --disable-video

make  

sudo make install  

