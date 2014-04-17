TO test
=======

lebih dari test

 Web Service
—Web Services : Merupakan istilah yang mengacu pada aplikasi virtual atau terdistribusi atau proses yang menggunakan internet untuk menghubungkan aktivitas atau komponen perangkat lunak.
—Web Service merupakan arsitektur komputasi yang terdistribusi. Arsitektur ini  bertujuan  untuk memungkinkan bermacam-macam aplikasi untuk saling komunikasi

Keuntungan yang didapat dalam menggunakan web service adalah semua aplikasi didunia dapat berkomunikasi satu dan lainnya . Komunikasi antar aplikasi ini tidak memiliki batasan tempat, sistem operasi, bahasa pemrograman, protokol dan lain sebagainya.

Untuk berkomunikasi dengan Web Service komputer klien akan
mengirimkan pesan SOAP yang Mengandung pemanggilan pada  sebuah
method beserta parameter yang di butuhkan (oleh method tersebut).
Sebagai tambahan, pesan SOAP dapat juga mengandung sejumlah item
Header yang menjelaskan kebutuhan klien lebih lanjut. 

arsitektur web service
—Web service memiliki tiga entitas dalam arsitekturnya, yaitu:
—1.  Service Requester (peminta layanan)
—2.  Service Provider (penyedia layanan)
—3.  Service Registry (daftar layanan)
—Service Provider: Berfungsi untuk menyediakan layanan/service dan mengolah sebuah registry agar layanan-layanan tersebut dapat tersedia.
—Service Registry: Berfungsi sebagai lokasi central yang mendeskripsikan semua layanan/service yang telah di-register.
—Service Requestor: Peminta layanan yang mencari dan menemukan layanan yang dibutuhkan serta menggunakan layanan tersebut.
operasi-operasi web service
—Secara umum, web service memiliki tiga operasi yang terlibat di dalamnya, yaitu:
—Publish/Unpublish: Menerbitkan/menghapus layanan ke dalam atau dari registry.
—Find: Service requestor mencari dan menemukan layanan yang dibutuhkan.
—Bind: Service requestor setelah menemukan layanan yang dicarinya, kemudian melakukan binding ke service provider untuk melakukan interaksi dan mengakses layanan/service yang disediakan oleh service provider.
komponen utama web service
—SOAP (Simple Object Access Protocol)
  SOAP merupakan spesifikasi yang mendefenisikan grammar XML untuk pesan yang akan dikirimkan dan juga jawaban dari pesan tersebut. Tujuan dari SOAP adalah untuk mendeskripsikan format sebuah pesan yang tidak bergantung pada perangkat keras dan perangkat lunak apapun, melainkan SOAP dapat membawa pesan dari sebuah platform ke platform lainnya tanpa adanya ambiguitas. SOAP biasanya terdiri dari dua bagian : header yang membawa instruksi pemprosesan dan body yang mengandung informasi yang ingin disampaikan.
—Extensible Markup Language (XML)— Merupakan bahasa dimana semua web service dibangun. XML merupakan alat untuk membangun dokumen self-describing. Dalam XML kita dapat membuat sendiri tag-tag dan komponen grammar lainnya.Grammar-grammar ini di deskripsikan dalam skema XML (XML schema) yang menentukan tags yang di izinkan (untuk digunakan) dan hubungan antar element yang didefenisikan oleh tags tersebut.

—Hypertext Transport Protocol (HTTP)—
  Merupakan protokol yang dibangun untuk memfasilitasi pertukaran data dari browser ke web server dan sebaliknya. Web service menggunakan protokol ini untuk memindahkan pesan SOAP dan dokumen WSDL dari satu komputer ke komputer lainnya.
Web Services Description Language (WSDL)— Merupakan spesifikasi yang menjelaskan sebuah perangkat lunak dalam kaitannya dengan pemanggilan method yang terdapat pada perangkat lunak tersebut. Method ini di deskripsikan dengan cara yang abstrak yang tidak bergantung pada bahasa pemrograman apa service tersebut di buat atau pada komputer dan sistem operasi apa ia berjalan.
—Universal Discovery Description Integration (UDDI)—UDDI menyediakan framework untuk mendeskripsikan dan menemukan web service yang tersedia di Web. UDDI menyediakan framework ini dengan menggunakan registri service berbasis web yang terdistribusi dan registri tersebut dapat diakses dengan menggunakan SOAP. Sederhanya UDDI merupakan mesin pencarian untuk web service. Semua penyedia web service menggunakan WSDL untuk mendeskripsikan aplikasi SOAP mereka. WSDL  ini kemudian di kirim ke pusat registri UDDI dan informasi ini dapat diakses oleh pencari web service.
membuat web service menggunakan PHP
—Library-> nuSOAP
—nuSOAP, merupakan library yang dibuat dengan bahasa PHP untuk mempermudah proses pembuatan dan juga pengaksesan web service dengan menggunakan bahasa PHP


BAKA TEST II
============


Layanan Web adalah sistem software yang didesain untuk mendukung interaksi interoperable mesin-ke-mesin melalui sebuah jaringan. Dalam konteks aplikasi Web, ia biasanya merujuk ke satu set API yang dapat diakses melalui Internet dan menjalankan layanan di hosting sitem remote. Sebagai contoh, klien berbasis-Flex dapat memanggil fungsi yang diimplementasikan pada sisi server yang menjalankan aplikasi berbasis-PHP. Layanan Web bergantung pada SOAP sebagai lapisan dasar tumpukan protokol komunikasinya.

Yii menyediakan CWebService dan CWebServiceAction untuk menyederhanakan pekerjaan implementasi layanan Web dalam aplikasi Web. APIs dikelompokkan ke dalam kelas, disebut service providers. Yii akan membuat sebuah spesifikasi WSDL untuk setiap kelas yang menjelaskan API apa yang bersifat variabel dan bagaimana ia harus dipanggil oleh klien. Ketika sebuah API dipanggil oleh klien, Yii akan menginisiasi penyedia layanan terkait dan memanggil API yang diminta guna memenuhi permintaan.

    Catatan: CWebService bergantung pada PHP SOAP extension. Pastikan Anda menghidupkannya sebelum mencoba menampilkan contoh dalam seksi ini.

1. Mendefinisikan Penyedia Layanan

Seperti sudah disebutkan di atas, penyedia layanan adalah kelas yang mendefinisikan metode yang dapat secara remote (jarak jauh) dipanggil. Yii bergantung pada komentar dokumen dan kelas refleksi dalam mengidentifikasi metode mana yang bisa dipanggil secara remote dan parameter apa serta nilai balik.

Mari kita mulai dengan kutipan layanan stok. Layanan ini mengijinkan klien untuk meminta kutipan stok yang sudah ditetapkan. Kita mendefinisikan penydia layanan sebagai berikut. Catatan bahwa kita mendefinisikan kelas penyedia StockController dengan memperluas CController. Ini tidak diperlukan. Kami akan segera menjelaskan mengapa kita melakukannya.

class StockController extends CController
{
    /**
     * @param string the symbol of the stock
     * @return float the stock price
     * @soap
     */
    public function getPrice($symbol)
    {
        $prices=array('IBM'=>100, 'GOOGLE'=>350);
        return isset($prices[$symbol])?$prices[$symbol]:0;
        //...return stock price for $symbol
    }
}

Dalam contoh di atas, kita mendeklarasikan metode getPrice menjadi API layanan Web, menandainya dengan tag @soap dalam komentar dokumen. Kita bergantung pada komentar dokumen untuk menetapkan jenis data parameter input dan nilai hasil. API tambahan dapat dideklarasikan dengan cara yang sama.
2. Mendeklarasikan Aksi Layanan Web

Setelah mendefinisikan penyedia layanan, kita harus membuatnya tersedia bagi klien. Sebenarnya kita ingin membuat aksi controller untuk mengekspos layanan. Ini bisa dilakukan secara mudah dengan mendeklarasikan aksi CWebServiceAction dalam kelas controller. Dalam contoh kita, kita akan memasukkan StockController.

class StockController extends CController
{
    public function actions()
    {
        return array(
            'quote'=>array(
                'class'=>'CWebServiceAction',
            ),
        );
    }
 
    /**
     * @param string the symbol of the stock
     * @return float the stock price
     * @soap
     */
    public function getPrice($symbol)
    {
        //...kembalikan harga stok untuk simbol $symbol
    }
}

Selesai, hanya itu yang kita perlukan dalam membuat layanan Web! Jika kita mencoba mengakses aksi dengan URL http://hostname/path/to/index.php?r=stock/quote, kita akan melihat banyak konten XML yang sebenarnya WSDL bagi layanan Web yang kita definisikan.

    Tip: Secara default, CWebServiceAction menganggap controller saat ini adalah penyedia layanan. Itulah mengapa kita mendefinisikan metode getPrice di dalam kelas StockController.

3. Menerima Layanan Web

Untuk melengkapi contoh, mari kita buat klien untuk menerima layanan Web yang baru kita buat. Contoh klien ditulis dalam PHP, tapi ia dapat dibuat dalam bahasa lainnya seperti Java, C#, Flex, dll.

$client=new SoapClient('http://hostname/path/to/index.php?r=stock/quote');
echo $client->getPrice('GOOGLE');

Jalankan skrip di atas baik dalam Web ataupun mode konsol, dan kita seharusnya melihat 350 yang merupakan harga untuk GOOGLE.
4. Tipe Data

Ketika mendeklarasikan metode kelas dan properti yang akan diakses secara remote, kita harus menetapkan tipe data atas parameter input dan output. Tipe data primitif berikut bisa dipakai:

    str/string: dipetakan ke xsd:string;
    int/integer: dipetakan ke xsd:int;
    float/double: dipetakan ke xsd:float;
    bool/boolean: dipetakan ke xsd:boolean;
    date: dipetakan ke xsd:date;
    time: dipetakan ke xsd:time;
    datetime: dipetakan ke xsd:dateTime;
    array: dipetakan ke xsd:string;
    object: dipetakan ke xsd:struct;
    mixed: dipetakan ke xsd:anyType.

Jika tipe bukan salah satupun dari tipe primitif di atas, ia dianggap sebagai tipe composite yang terdiri dari properti. Tipe composite disajikan dalam batasan kelas, dan propertinya adalah variabel anggota public kelas yang ditandai dengan @soap dalam komentar dokumennya.

Kita juga bisa menggunakan tipe array dengan menambahkan [] di akhir tipe primitif atau tipe composite. Ini akan menetapkan sebuah array pada tipe yang sudah ditetapkan tersebut.

Di bawah ini adalah contoh mendefinisikan Web API getPosts Web API yang menghasilkan array obyek Post.

class PostController extends CController
{
    /**
     * @return Post[] a list of posts
     * @soap
     */
    public function getPosts()
    {
        return Post::model()->findAll();
    }
}
 
class Post extends CActiveRecord
{
    /**
     * @var integer post ID
     * @soap
     */
    public $id;
    /**
     * @var string post title
     * @soap
     */
    public $title;
 
    public static function model($className=__CLASS__)
    {
        return parent::model($className);
    }
}

5. Pemetaan Kelas

Agar bisa menerima parameter tipe composite dari klien, aplikasi harus mendeklarasikan pemetaan dari tipe WSDL ke kelas PHP terkait. Ini dilakukan dengan mengkonfigurasi properti classMap pada CWebServiceAction.

class PostController extends CController
{
    public function actions()
    {
        return array(
            'service'=>array(
                'class'=>'CWebServiceAction',
                'classMap'=>array(
                    'Post'=>'Post',  // atau cukup 'Post'
                ),
            ),
        );
    }
    ......
}

6. Mengintersepsi Penyertaan Metode Remote

Dengan mengimplementasi antar muka IWebServiceProvider, penyedia layanan bisa mengintersepsi penyertaan metode jarak jauh. Dalam IWebServiceProvider::beforeWebMethod, penyedia bisa mengambil instance CWebService saat ini dan mendapatkan nama metode yang saat ini sedang dipakai via CWebService::methodName. Ini dapat menghasilkan false jika metode remote seharusnya tidak dipanggil untuk beberapa alasan (misalnya akses tidak diotorisasi).
