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

#如何安装zbar
sudo yum -y install pdftk ImageMagick ImageMagick-devel ghostscript Python-imaging python-devel python-gtk2-dev libqt4-dev 
wget http://downloads.sourceforge.net/project/zbar/zbar/0.10/zbar-0.10.tar.gz  
tar -zvxf zbar-0.10.tar.gz  
cd zbar-0.10
./configure --without-imagemagick –disable-video –without-qt –without-gtk –without-x   
make  
sudo make install  

