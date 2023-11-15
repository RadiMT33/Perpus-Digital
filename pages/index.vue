<template>
  <br>
  <h2>Riwayat Kunjungan</h2>
  <NuxtLink to="/tambah" class="btn btn-outline-secondary">Isi buku Tamu</NuxtLink>
  <div>
    <br>
    <table class="table table-striped">
      <thead class="table-dark">
        <tr>
          <th>#</th>
          <th>TANGGAL DAN WAKTU</th>
          <th>NAMA</th>
          <th>ANGGOTA</th>
          <th>KEPERLUAN</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="pengunjung in visitors" :key="pengunjung.id">
          <td>{{ Pengunjung.id }}</td>
          <td>{{ pengunjung.tanggal }}</td>
          <td>{{ pengunjung.nama }}</td>
          <td>{{ pengunjung.anggota }}</td>
          <td>{{ pengunjung.keperluan }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup>
const client =useSupabaseClient();
const visitors = ref([]);

async function getdata() {
  const { data, error } = await client.from("pengunjung").select("*");
  if (data) visitors.value = data;
}
onMounted(()=> getdata());
</script>
