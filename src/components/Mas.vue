<template>
  <div>
    <div class="buttons">
      <button @click="filterData('serial')">Serial</button>
      <button @click="filterData('anime')">Anime</button>
      <button @click="filterData('film')">Film</button>
    </div>
    
    <div class="inf">
      <div 
        v-for="item in filteredData" 
        :key="item.judul" 
        class="card" 
        @click="tampilkanData(item.judul, item.informasi)"
      >
        <span></span>
        <div class="content">
          <img :src="item.gambar" alt="gambar" class="gambar">
        </div>
      </div>
    </div>

    <div v-if="dataTerpilih" class="tampilan-data">
      <h2>{{ dataTerpilih.judul }}</h2>
      <p>{{ dataTerpilih.informasi }}</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      dataTerpilih: null,
      currentFilter: 'serial',
      items: [
        {
          judul: 'LTNS',
          informasi: 'Drama Korea berjudul LTNS (Long Time No Sex) adalah drama terbaru yang memiliki 6 episode. Drama ini sudah tayang sejak 19 Januari 2024 lalu. Diarahkan dan ditulis oleh Lim Dae Hyung, drama ini memiliki genre komedi romantis.',
          gambar: 'https://encrypted-tbn2.gstatic.com/images?q=tbn:ANd9GcRRWPOdMqTPDsmMjhVQaw6_0wo7VueaA3AxRpMN1wpqSzv0vp9n',
          kategori: 'serial'
        },
        {
          judul: 'Blue Lock',
          informasi: 'Blue Lock adalah sebuah seri manga shōnen Jepang yang ditulis oleh Muneyuki Kaneshiro dan diilustrasikan oleh Yūsuke Nomura. Manga ini mulai dimuat dalam majalah Weekly Shōnen Magazine terbitan Kodansha sejak bulan Agustus 2018, dan telah dibundel menjadi dua puluh sembilan volume tankōbon.',
          gambar: 'https://encrypted-tbn3.gstatic.com/images?q=tbn:ANd9GcTwgSYjwQw9emH9C-cjovzO1Sqm_UpSZL_8eY4o_yLr3QmroH7k',
          kategori: 'anime'
        },
        {
          judul: 'Jujutsu Kaisen',
          informasi: 'Jujutsu Kaisen menceritakan sosok Yuji Itadori yang secara tidak sengaja memanggil makhluk mistis. Pemanggilan terjadi karena siswa SMA ini mengutak-atik sebuah benda terkutuk. Kemunculan makhluk ini berakibat fatal, hingga Itadori harus menyelamatkan nyama teman-temannya.',
          gambar: 'https://encrypted-tbn1.gstatic.com/images?q=tbn:ANd9GcTMxM0RXhfwPC_6lM9UaqCP8y_RQPyY-Iu2pqFbO5Loi9sAQvgb',
          kategori: 'anime'
        },
        {
          judul: 'The Terminal List',
          informasi: 'The Terminal List adalah serial televisi thriller aksi Amerika yang dibuat oleh David DiGilio, berdasarkan novel Jack Carr tahun 2018 dengan nama yang sama. Serial ini bercerita tentang seorang Navy SEAL yang berusaha membalas pembunuhan keluarganya.',
          gambar: 'https://encrypted-tbn1.gstatic.com/images?q=tbn:ANd9GcRN1GLAsnoPctHSTXo1qCenKQrvTAs9wb_vJi7M4Ob5rj3g5Ny7',
          kategori: 'serial'
        },
        {
          judul: 'Vina Sebelum 7 Hari',
          informasi: 'Jenazah Almarhumah Vina (Nayla Purnama) yang ditemukan di flyover Cirebon dianggap mengalami kecelakaan motor tunggal. Nenek Vina (Lydia Kandou) curiga karena tubuh Vina remuk tak wajar namun tak punya cukup bukti untuk menolak berita acara. Vina merasuki tubuh sahabatnya Linda (Gisellma Firmansyah), Ia hanya punya waktu sebelum 7 hari usai kematiannya untuk mengungkap kebenaran yang menyakitkan. Alfatihah..',
          gambar: 'https://cdn.cgv.id/uploads_v2/movie/compressed/24010700.jpg',
          kategori: 'film'
        },
        {
          judul: 'Dilan 1983 who ai ni',
          informasi: 'Dilan 1983: Wo Ai Ni memang menceritakan kisah masa kecil Dilan yang tinggal di Bandung bersama keluarganya. Film ini dijamin bisa membawa penonton kembali ke masa 1980-an, di mana melihat sisi lain Dilan yang belum pernah terungkap pada cerita sebelumnya.',
          gambar: 'https://inforadar.disway.id/upload/0f655f579c3577c75ac8093050869d2f.jpg',
          kategori: 'film'
        },
        {
          judul: 'Tuhan Izinkan Aku Berdosa',
          informasi: 'Tuhan, Izinkan Aku Berdosa bercerita tentang Kiran, seorang mahasiswi dari keluarga miskin yang taat beragama dan kritis tapi terjebak di kelompok agama garis keras yang dipimpin Abu Dharda. Setelahnya ia malah mendapatkan kekecewaan dan ujian yang bertubi-tubi.',
          gambar: 'https://hypeabis.id/assets/content/202405221703171716372197.jpg',
          kategori: 'film'
        },
        {
          judul: 'Avatar The Last Air Bender',
          informasi: 'Seorang anak laki-laki yang dikenal sebagai Avatar harus menguasai empat kekuatan elemen untuk menyelamatkan dunia yang sedang berperang — dan melawan musuh kejam yang bertekad menghentikannya.',
          gambar: 'https://m.media-amazon.com/images/I/81WmTJU0i4L._AC_UF894,1000_QL80_.jpg',
          kategori: 'serial'
        },
        {
          judul: 'The Tale of the Princess Kaguya',
          informasi: 'Ditemukan dalam batang bambu oleh seorang pemotong bambu dan istrinya, seorang gadis kecil tumbuh menjadi seorang gadis yang menawan. Putri muda yang misterius itu memukau semua yang memandangnya, namun ia harus menemui takdirnya, untuk menebus kejahatan yang ia lakukan.',
          gambar: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTQi1PUzRRw2aPGeDGl9vSDuQ3yMLIgHpJOIVSjed8PHD2wWQpl',
          kategori: 'anime'
        },
      ]
    };
  },
  computed: {
    filteredData() {
      return this.items.filter(item => item.kategori === this.currentFilter);
    }
  },
  methods: {
    tampilkanData(judul, informasi) {
      if (this.dataTerpilih && this.dataTerpilih.judul === judul) {
        this.dataTerpilih = null;
      } else {
        this.dataTerpilih = { judul, informasi };
      }
    },
    filterData(kategori) {
      this.currentFilter = kategori;
      this.dataTerpilih = null; // Reset data terpilih ketika mengubah filter
    }
  }
};
</script>

<style>
.buttons {
  display: flex;
  justify-content: center;
  margin-bottom: 20px;
}
.buttons button {
  margin: 0 10px;
  padding: 10px 20px;
  cursor: pointer;
}
.tampilan-data {
  position: fixed;
  bottom: 25px;
  right: 25px; /* Ubah posisi right ke 25px */
  max-width: 300px; /* Sesuaikan lebar maksimum sesuai kebutuhan */
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 8px;
  background-color: #f9f9f9;
  box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.1);
}
</style>
