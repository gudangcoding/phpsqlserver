# phpsqlserver
1 - Unduh drivernya di sini https://go.microsoft.com/fwlink/?linkid=2226724<br>
2 - ekstrak dan pindahkan ke folder c:\xampp\php\ext<br>
3 - kemudian aktifkan xampp klik kanan tombol config pada apache dan pilih php.ini<br>
    Tambahkan baris berikut, seuaikan dengan php berapa yang di pakai contoh disini saya menggunakan php 80<br>
    extension=php_sqlsrv_80_ts.dll<br>
    extension=php_pdo_sqlsrv_80_ts.dll<br>
4 - restart xampp nya<br>
5- pastikan file database.php seperti ini<br>
<code>
    <?php
   $this->pdo = new PDO(
            DRIVER_DB.":server=".HOST.";
            Database=".DATABASE_NAME."",
            DB_USERNAME,
            DB_PASSWORD,
            array(
                //PDO::ATTR_PERSISTENT => true,
                PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION
            )
    );
?>
 </code>
 
6 - buat file koneksi dan tulis kode seperti set attribut server<br>

<code>
    <?php
        ini_set( "display_errors", true );
        define( "HOST", "DESKTOP-I8N66OQ" );
        //nama database
        define( "DRIVER_DB", "sqlsrv" );
        //nama database
        define( "DATABASE_NAME", "tes_sqlsrv" );
        define( "DB_USERNAME", "sa" );
        //password mysql
        define( "DB_PASSWORD", "123" );
        define('DB_CHARACSET', 'utf8');
        require_once ('Database.php');
        $db = new Database();
        function handleException( $exception ) {
          echo  $exception->getMessage();
        }
        set_exception_handler( 'handleException' );
    ?>
 </code>  
 
 7 -  cara pakai<br>
 
 <code>
      <?php
        include"config.php";
        $data = [];
        $query = $db->fetch_custom("select * from namatabel ");
        foreach ($query as $a) {
            $data[] = $a;
        }
        echo json_encode($data);
</code>
<br>

semoga bermanfaat
