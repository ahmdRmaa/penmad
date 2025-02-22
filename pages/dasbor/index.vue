<template>
    <div class="container mt-4">
      <h1>Edit Berita</h1>
      <form @submit.prevent="updateNews">
        <div class="mb-3">
          <label for="title" class="form-label">Judul Berita</label>
          <input 
            type="text" 
            class="form-control" 
            id="title" 
            v-model="title" 
            required
          />
        </div>
        
        <div class="mb-3">
          <label for="content" class="form-label">Konten Berita</label>
          <textarea 
            class="form-control" 
            id="content" 
            v-model="content" 
            rows="4" 
            required
          ></textarea>
        </div>
        
        <div class="mb-3">
          <label for="image" class="form-label">Upload Gambar</label>
          <input 
            type="file" 
            class="form-control" 
            id="image" 
            @change="onFileChange" 
            accept="image/*"
          />
        </div>
  
        <div v-if="imagePreview" class="mb-3">
          <h5>Preview Gambar</h5>
          <img :src="imagePreview" alt="Image Preview" class="img-fluid" style="max-width: 200px;">
        </div>
  
        <div v-if="errorMessage" class="alert alert-danger" role="alert">
          {{ errorMessage }}
        </div>
  
        <button type="submit" class="btn btn-primary">Simpan Perubahan</button>
      </form>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        title: '',
        content: '',
        image: null,
        imagePreview: null,
        errorMessage: '',
      };
    },
    methods: {
      updateNews() {
        // Validasi sederhana
        if (!this.title || !this.content) {
          this.errorMessage = 'Judul dan konten berita tidak boleh kosong!';
          return;
        }
  
        // Menangani proses update berita
        const formData = new FormData();
        formData.append('title', this.title);
        formData.append('content', this.content);
  
        if (this.image) {
          formData.append('image', this.image);
        }
  
        // Simulasi pengiriman data ke API atau server
        console.log('Data Berita yang Dikirim:', formData);
  
        // Reset form setelah berhasil (contoh)
        this.title = '';
        this.content = '';
        this.image = null;
        this.imagePreview = null;
        this.errorMessage = '';
        alert('Berita berhasil diperbarui!');
      },
  
      onFileChange(event) {
        const file = event.target.files[0];
        if (file) {
          this.image = file;
  
          // Menampilkan preview gambar
          const reader = new FileReader();
          reader.onload = (e) => {
            this.imagePreview = e.target.result;
          };
          reader.readAsDataURL(file);
        }
      },
    },
  };
  </script>
  
  <style scoped>
  /* Gaya tambahan untuk halaman dashboard */
  img {
    max-width: 100%;
    height: auto;
  }
  </style>
  