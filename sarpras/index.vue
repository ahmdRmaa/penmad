<template>
    <div class="container mt-4">
      <h1>Sarana dan Prasarana Kementerian Agama</h1>
  
      <!-- Tombol Tambah Sarana dan Prasarana -->
      <button @click="showAddModal" class="btn btn-primary mb-3">Tambah Sarana dan Prasarana</button>
  
      <!-- Daftar Sarana dan Prasarana -->
      <div v-if="saranaPrasaranaList.length" class="list-group">
        <div 
          v-for="(item, index) in saranaPrasaranaList" 
          :key="item.id" 
          class="list-group-item d-flex justify-content-between align-items-center">
          <div>
            <h5>{{ item.name }}</h5>
            <p>{{ item.description }}</p>
            <p><strong>Lokasi:</strong> {{ item.location }}</p>
          </div>
  
          <div>
            <button 
              class="btn btn-warning btn-sm me-2" 
              @click="editItem(item)">
              Edit
            </button>
            <button 
              class="btn btn-danger btn-sm" 
              @click="deleteItem(item.id)">
              Hapus
            </button>
          </div>
        </div>
      </div>
  
      <!-- Modal Add/Edit Sarana dan Prasarana -->
      <div v-if="showModal" class="modal fade show" tabindex="-1" style="display: block;">
        <div class="modal-dialog">
          <div class="modal-content">
            <div class="modal-header">
              <h5 class="modal-title">{{ isEditMode ? 'Edit' : 'Tambah' }} Sarana dan Prasarana</h5>
              <button type="button" class="btn-close" @click="closeModal"></button>
            </div>
            <div class="modal-body">
              <form @submit.prevent="isEditMode ? updateItem() : addItem()">
                <div class="mb-3">
                  <label for="itemName" class="form-label">Nama Sarana/Prasarana</label>
                  <input 
                    type="text" 
                    id="itemName" 
                    class="form-control" 
                    v-model="itemName" 
                    required
                  />
                </div>
                <div class="mb-3">
                  <label for="itemDescription" class="form-label">Deskripsi</label>
                  <textarea 
                    id="itemDescription" 
                    class="form-control" 
                    v-model="itemDescription" 
                    required
                  ></textarea>
                </div>
                <div class="mb-3">
                  <label for="itemLocation" class="form-label">Lokasi</label>
                  <input 
                    type="text" 
                    id="itemLocation" 
                    class="form-control" 
                    v-model="itemLocation" 
                    required
                  />
                </div>
                <div class="modal-footer">
                  <button type="button" class="btn btn-secondary" @click="closeModal">Tutup</button>
                  <button type="submit" class="btn btn-primary">
                    {{ isEditMode ? 'Perbarui' : 'Simpan' }}
                  </button>
                </div>
              </form>
            </div>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        showModal: false,
        isEditMode: false,
        saranaPrasaranaList: [
          { id: 1, name: 'Gedung A', description: 'Gedung utama Kementerian Agama', location: 'Jakarta' },
          { id: 2, name: 'Peralatan Audio Visual', description: 'Peralatan untuk acara seminar dan pertemuan', location: 'Surabaya' },
        ],
        itemName: '',
        itemDescription: '',
        itemLocation: '',
        currentItemId: null,
      };
    },
    methods: {
      // Tampilkan modal untuk menambah sarana dan prasarana
      showAddModal() {
        this.showModal = true;
        this.isEditMode = false;
        this.itemName = '';
        this.itemDescription = '';
        this.itemLocation = '';
      },
  
      // Menutup modal
      closeModal() {
        this.showModal = false;
      },
  
      // Menambahkan sarana dan prasarana baru
      addItem() {
        const newItem = {
          id: Date.now(), // Menggunakan timestamp sebagai ID unik
          name: this.itemName,
          description: this.itemDescription,
          location: this.itemLocation,
        };
        this.saranaPrasaranaList.push(newItem);
        this.closeModal();
      },
  
      // Mengedit sarana dan prasarana yang sudah ada
      editItem(item) {
        this.isEditMode = true;
        this.showModal = true;
        this.itemName = item.name;
        this.itemDescription = item.description;
        this.itemLocation = item.location;
        this.currentItemId = item.id;
      },
  
      // Memperbarui sarana dan prasarana yang ada
      updateItem() {
        const updatedItem = {
          id: this.currentItemId,
          name: this.itemName,
          description: this.itemDescription,
          location: this.itemLocation,
        };
  
        const index = this.saranaPrasaranaList.findIndex(item => item.id === this.currentItemId);
        if (index !== -1) {
          this.saranaPrasaranaList.splice(index, 1, updatedItem);
        }
  
        this.closeModal();
      },
  
      // Menghapus sarana dan prasarana
      deleteItem(id) {
        this.saranaPrasaranaList = this.saranaPrasaranaList.filter(item => item.id !== id);
      },
    },
  };
  </script>
  
  <style scoped>
  .modal {
    display: block;
    z-index: 1050;
  }
  </style>
  