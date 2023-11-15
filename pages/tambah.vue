<template>
<div class="row">
    <div class="col">
        <h2><center>isi pengunjung</center></h2>
        <div v-if="sukses" class="alert alert-succes">berhasil simpan</div>
        <form @submit.prevent="simpan()">
        <div class="mb-3">
            <select v-models="form.anggota" class="from-control">
            <option value="">pilih keanggotaan</option>
            <option value="SISWA">SISWA</option>
            <option value="GURU">GURU</option>
            <option value="STAFF">STAFF</option>
        </select>
        </div>
        <div v-if="form.anggota == 'SISWA'" class="mb-3">
            <input v-model="from.kelas" type="text" class="from-control" placeholder="kelas">
        </div>
        <div class="mb-3">
            <texarea v-model="from.keperluan" cols="30" rows="10" placeholder="keperluan" class="from-control"></texarea>
        </div>
        <button type="submit" class="btn btn-outline-primary">kirim</button>
        <NuxtLink to="/">kembali</NuxtLink>
    </form></div>
    </div>
</template>

<script setup>
const supabase = useSupabaseClient();
const form = reactive({ 
    nama: "", 
    anggota: "", 
    kelas: "",
    keperluan: ""
})
const sukses = ref(false)

async function simpan(){
    sukses.value=false
    const {error}= await supabase
    .from('penggunjung')
    .insert(from)
    if (data){
        sukses.value=true
    }
}

async function getanggota(){
    const { data, error } = await supabase.from("anggota").select();
    if (data) anggota.value = data;
}
async function Simpankunjungan(){
    const { error } = await supabase
    .from('pengunjung')
    .insert(form);
}
onMounted(() => getanggota());
</script>
