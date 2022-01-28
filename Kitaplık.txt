#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <time.h>
#include <windows.h>
typedef struct{
	
	char isim[30];
	char yazar[30];
	int sayfasayisi;
	char yayinevi[15];
	
}kitaplik;

void kitapekle(kitaplik *kitaplar,int adet)
{
	int kontrol=0;
	int devam,i=0;
	while(i<adet)
	{
		if(kontrol==*kitaplar[i].isim)
		{
			printf("Kitabin ad,yazar,sayfa sayisi ve yayinevi bilgilerini girin:(Isimleri yazarken bosluk kullanmayin)\n",i+1);
			scanf("%s%s%d%s",&kitaplar[i].isim,&kitaplar[i].yazar,&kitaplar[i].sayfasayisi,&kitaplar[i].yayinevi);	
		
			printf("Kitap eklendi.Devam etmek icin 1 yazin(Cikmak icin 0):");
			scanf("%d",&devam);
			i++;
			
			if(devam)
			{
				if(i>=adet)
				{
					printf("Kitapligi doldurdunuz.Daha fazla ekleyemezsiniz!(Limiti %d olarak belirlemistiniz)\n",adet);
					printf("Menuye yonlendiriliyorsunuz...\n");
					sleep(3);	
				}
				continue;
			}
			else
			{
				printf("Menuye yonlendiriliyorsunuz...");
				sleep(3);
				break;
			}	
		}
		i++;
		if(i==adet)
		{
			printf("Kitapligi doldurdunuz.Daha fazla ekleyemezsiniz!(Limiti %d olarak belirlemistiniz)\n",adet);
			printf("Menuye yonlendiriliyorsunuz...\n");
			sleep(3);
		}
	}
}

int kitapara(kitaplik *kitaplar,int adet,char *aranan)
{
	int index,i,arama;
	
	for(i=0;i<adet;i++)
	{
		arama=strcmp(aranan,kitaplar[i].isim);
		if(arama==0)//Tamamen aynıysa 0 döner
		{
			index=i;
			return index;
		}
	}
	
	if(arama!=0)
	{
		return -1;
	}

}

void tumkitaplar(kitaplik *kitaplar,int adet)
{
	int i;
	
	for(i=0;i<adet;i++)
	{
		printf("%d.Kitap-%s,%s,%d,%s\n",i+1,kitaplar[i].isim,kitaplar[i].yazar,kitaplar[i].sayfasayisi,kitaplar[i].yayinevi);
	}
	
}

int main(int argc, char *argv[]) {
	
	int adet,secim,i,uyku;
	kitaplik *kitaplar;
	char *aranan;
	
	aranan=(char *)malloc(sizeof(char));
	
	printf("Kitapligin buyuklugunu girin:");
	scanf("%d",&adet);
	
	kitaplar=(kitaplik*)calloc(adet,sizeof(kitaplik));

	while(1)
	{
	printf("-----------MENU------------\n");
	printf("1)Kitap Ekle\n");
	printf("2)Kitap Ara\n");
	printf("3)Tum Kitaplari Goruntule\n");
	printf("Secim Yapin(Cikmak icin 0):");
	scanf("%d",&secim);
	system("cls");
	
	switch(secim)
	{
		case 0:
			goto cikis;
			break;
		case 1:
			kitapekle(kitaplar,adet);
			system("cls");
			break;
		case 2:
			printf("Aranacak kitabin adini girin:");
			scanf("%s",aranan);
			int aramasonuc=kitapara(kitaplar,adet,aranan);
			
			if(aramasonuc!=-1)
			{
			printf("Kitap bulunmustur.Kitap bilgileri:\n");
			printf("Ad:%s\n",kitaplar[aramasonuc].isim);
			printf("Yazar:%s\n",kitaplar[aramasonuc].yazar);
			printf("Sayfa Sayisi:%d\n",kitaplar[aramasonuc].sayfasayisi);
			printf("Yayinevi:%s\n",kitaplar[aramasonuc].yayinevi);		
			}
			if(aramasonuc==-1)
			{
				printf("Kitap bulunamamistir.Menuye yonlendiriliyorsunuz\n");
				sleep(3);
				system("cls");
			}
			break;
		case 3:
			printf("Tum kitaplar:\n");
			for(i=0;i<adet;i++)
			{
				printf("%d.Kitap bilgileri:%s,%s,%d,%s\n",i+1,kitaplar[i].isim,kitaplar[i].yazar,kitaplar[i].sayfasayisi,kitaplar[i].yayinevi);
			}
			
			printf("Menuye gecmek icin 0i tuslayin");
			scanf("%d",&uyku);
			sleep(uyku);
			system("cls");
			break;
		default:
			printf("Yanlis islem tusladiniz.\n");
			system("cls");
			break;	
			}	
	}
	
	cikis:
		
	return 0;
}
