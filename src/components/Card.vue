<template>
    <div class="card shadow-lg p-3 mb-5 bg-white rounded">
        <div class="text-center">
             <h4>Bantuan Komplek Panghegar</h4>
        <span>Sebuah Area di Wilayah Kelurahan Cipadung Kulon, Kecamatan Panyileukan</span>
        </div>
        <div class="mt-3">
            <b-form @submit="onSubmit" @reset="onReset" >
            <div class="row mb-2">
                <div class="col-lg-6 col-md-8 col-sm-12">
                    <b-form-group
                    id="Nama"
                    label="Nama :"
                    class="mb-0"
                    label-for="input-nama"
                >
                    <b-form-input
                    id="input-nama"
                    v-model="form.name"
                    type="text"
                    oninvalid="setCustomValidity('Nama tidak boleh kosong')"
                    oninput="setCustomValidity('')"
                    placeholder="Enter Name"
                    required
                    ></b-form-input>
                </b-form-group>
                </div>
            </div>
            <div class="row">
                <div class="col-lg-6 col-md-8 col-sm-12">
                    <b-form-group id="nik" label="NIK :" label-for="input-nik"  class="mb-0">
                        <b-form-input
                        id="input-nik"
                        v-model="form.nik"
                        placeholder="Ex. 12199221112"
                        required
                        oninvalid="setCustomValidity('NIK tidak boleh kosong')"
                        oninput="setCustomValidity('')"
                        type="number"
                        ></b-form-input>
                    </b-form-group>
                </div>
            </div>
            <div class="row">
                <div class="col-lg-6 col-md-8 col-sm-12">
                    <b-form-group id="nkk" label="Nomor Kartu Keluarga :" label-for="input-nkk">
                        <b-form-input
                        id="input-nkk"
                        v-model="form.nkk"
                        oninvalid="setCustomValidity('Nomor Kartu Keluarga tidak boleh kosong')"
                        oninput="setCustomValidity('')"
                        type="number"
                        required
                        ></b-form-input>
                    </b-form-group>
                </div>
            </div>

            <div class="row mb-2">
                <div class="col-md-6">
                    <b-form-group  label="Foto KTP :" label-for="input-ktp" class="mb-0">
                        <b-form-file id="ktp" v-model="form.ktp" ref="file-input-ktp" class="mb-2"  accept="image/jpeg, image/png, image/jpg, image/bmp" @change="changePhoto"></b-form-file>
                    </b-form-group>
                    <span class="text-danger" v-if="show && error.ktp">{{error.ktp}}</span>
                </div>
            </div>
            <div class="row mb-2">
                <div class="col-md-6">
                    <b-form-group label="Foto Kartu Keluarga :" label-for="input-kk" class="mb-0">
                        <b-form-file id="kk" v-model="form.kk" ref="file-input-kk" class="mb-2"  accept="image/jpeg, image/png, image/jpg, image/bmp" @change="changePhoto"></b-form-file>
                    </b-form-group>
                    <span class="text-danger" v-if="show && error.kk">{{error.kk}}</span>
                </div>
            </div>

            <div class="row mb-2" >
                <div class="col-lg-2 col-md-4 col-sm-6">
                    <b-form-group id="umur" label="Umur :" label-for="input-umur" class="mb-0">
                        <b-form-input
                        id="input-umur"
                        v-model="form.umur"
                        type="number"
                        oninvalid="setCustomValidity('Umur tidak boleh kosong')"
                        oninput="setCustomValidity('')"
                        required
                        ></b-form-input>
                    </b-form-group>
                    <span class="text-danger" v-if="show && error.umur">{{error.umur}}</span>
                </div>
            </div>
            <div class="row mt-4">
                <div class="col-md-6">
                    <b-form-group id="jk" label="Jenis Kelamin :" class="mb-0">
                         <b-form-radio-group
                            v-model="form.jenis_kelamin"
                            :options="optionJK"
                            class="mb-3"
                            value-field="item"
                            text-field="name"
                            disabled-field="notEnabled"
                            ></b-form-radio-group>
                    </b-form-group>
                   
                </div>
            </div>
            <div class="row">
               <div class="col-md-10 col-sm-12">
                   <b-form-group id="alamat" label="Alamat" label-for="input-umur">
                        <b-form-textarea
                            id="input-alamat"
                            v-model="form.alamat"
                            placeholder="Enter Alamat"
                            rows="3"
                            required
                            oninvalid="setCustomValidity('Alamat tidak boleh kosong')"
                            oninput="setCustomValidity('')"
                            max-rows="6"
                        ></b-form-textarea>
                    </b-form-group>
               </div> 
            </div>

            <div class="row">
                <div class="col-md-4">
                    <b-form-group
                    id="rt"
                    label="RT :"
                    label-for="input-rt"
                    >
                        <b-form-input
                        id="input-rt"
                        v-model="form.rt"
                        type="text"
                        placeholder="RT 0/00"
                        required
                        oninvalid="setCustomValidity('RT tidak boleh kosong')"
                        oninput="setCustomValidity('')"
                        ></b-form-input>
                    </b-form-group>
                </div>
                <div class="col-md-4">
                    <b-form-group
                    id="rw"
                    label="RW :"
                    label-for="input-rw"
                    >
                        <b-form-input
                        id="input-rw"
                        v-model="form.rw"
                        type="text"
                        placeholder="RW 0/00"
                        oninvalid="setCustomValidity('RW tidak boleh kosong')"
                        oninput="setCustomValidity('')"
                        required
                        ></b-form-input>
                    </b-form-group>
                </div>
            </div>

            <div class="row">
                <div class="col-md-6">
                    <b-form-group id="seblum-pandemi" label="Penghasilan Sebelum Pandemi :" label-for="input-sebelum-pandemi">
                        <b-input-group prepend="Rp" class="mb-2 mr-sm-2 mb-sm-0">
                            <b-form-input
                            id="input-sebelum-pandemi"
                            v-model="form.beforePandemi"
                            type="number"
                            required
                            oninvalid="setCustomValidity('Penghasilan tidak boleh kosong')"
                            oninput="setCustomValidity('')"
                            ></b-form-input>
                        </b-input-group>
                    </b-form-group>
                </div>
                <div class="col-md-6">
                    <b-form-group id="sesudah-pandemi" label="Penghasilan Setelah Pandemi :" label-for="input-sesudah-pandemi">
                        <b-input-group prepend="Rp" class="mb-2 mr-sm-2 mb-sm-0">
                            <b-form-input
                            id="input-sesudah-pandemi"
                            v-model="form.afterPandemi"
                            type="number"
                            required
                            oninvalid="setCustomValidity('Penghasilan tidak boleh kosong')"
                            oninput="setCustomValidity('')"
                            ></b-form-input>
                        </b-input-group>
                    </b-form-group>
                </div>
            </div>

            <div class="row mb-3">
                <div class="col-lg-6 col-md-8 col-sm-12">
                     <b-form-group id="alasan" label="Alasan membutuhkan bantuan" label-for="input-alasan">
                        <b-form-select v-model="form.alasan" :options="options" class="mt-3" @change="func_lainnya">
                            <template #first>
                                <b-form-select-option :value="null" disabled>-- PILIH ALASAN --</b-form-select-option>
                            </template>   
                        </b-form-select>
                     </b-form-group>
                     <b-toast id="toast-lainnya" static variant="warning">
                            Silahkan isi Alasan lainnya
                    </b-toast>
                     <b-form-input
                        v-if="form.alasan == 4"
                        id="lainnya"
                        size="sm"
                        title="Tulis Alasannya"
                        v-model="lainnya"
                        type="text"
    
                        ></b-form-input>
                        <span class="text-danger" v-if="show && error.alasan">{{error.alasan}}</span> 
                </div>
            </div>
            <div class="row">
                <div class="col-md-12">
                    <label for="checkbox" class="ft-12">
                        <input type="checkbox" v-model="form.check">
                        Saya menyatakan bahwa data yang diisikan adalah benar dan siap mempertanggungjawabkan apabila ditemukan ketidaksesuaian dalam data tersebut.
                    </label>
                </div>
            </div>
      <b-button type="submit" variant="primary" class="mr-2" :disabled="isDisable">Submit</b-button>
      <b-button type="reset" variant="danger">Reset</b-button>
    </b-form>
        </div>
    </div>
</template>
<script>
export default {
    name: 'Card',
    data() {
      return {
        isDisable: true,
        error: {
            umur: '',
            ktp: '',
            alasan: ''
        },
        form: {
          check: false,
          name: '',
          nik: '',
          nkk: '',
          umur: 25,
          alamat: '',
          alasan: '',
          rt: '',
          rw: '',
          jenis_kelamin: 'P',
          beforePandemi: 0,
          afterPandemi: 0,
          kk: null,
          ktp: null,
        },
         options: [
              {value : 1, text: 'Kehilangan pekerjaan'},
              {value : 2, text: 'Kepala Keluarga terdampak atau korban Covid'},
              {value : 3, text: 'Tergolong fakir/miskin semenjak sebelum Covid'},
              {value : 4, text: 'Lainnya'},

          ],
          optionJK: [
              {item: 'P', name: 'Perempuan'},
              {item: 'L', name: 'Laki-laki'}
          ],
          lainnya: '',
          show: false
      }
    },
    watch: {
        'form.umur'(){
            if(this.form.umur >= 25) {
                this.error.umur = ''
            }
        },
        'form.check'(val) {
            if(val) {
                this.isDisable = false
            } else {
                this.isDisable = true
            }
        },
        lainnya(){
           this.error.alasan = ''
        }
    },
    methods: {
        func_lainnya(item) {
             this.error.alasan = ''
           if(item == 4) {
                document.getElementById('lainnya').focus()
                this.$bvToast.show('toast-lainnya')
                this.hideToast()
           } 
        },
        hideToast() {
            setTimeout(()=> {
                this.$bvToast.hide('toast-lainnya')
            }, 2000)
        },
        checkPhoto(item) {
            if (item.size > 20987904) {
               return false
            }
            return true
        },
        changePhoto(item) {
            const id = item.target.id
            this.error[id] = ''
        },
      onSubmit(event) {
          this.show = true
          if(this.form.umur < 25) {
              this.error.umur = 'Umur tidak mencukupi'
              return false
          }
          
         if(this.form.ktp) {
          const size = this.checkPhoto(this.form.ktp)
          if (!size) {
              this.form.ktp = null
              this.error.ktp = 'Ukuran foto melembihi 2MB'
              return false
          }
         } else {
             this.error.ktp = 'Mohon Upload KTP'
         }

         if(this.form.kk) {
          const size = this.checkPhoto(this.form.kk)
          if (!size) {
              this.form.kk = null
              this.error.kk = 'Ukuran foto melembihi 2MB'
              return false
          }
         } else {
            this.error.kk = 'Mohon Upload KK' 
         }
         if(this.form.alasan) {
             if(this.form.alasan == 4) {
                 this.error.alasan = this.lainnya ? '' : 'Silahkan isi alasan membutuhkan bantuan'
             }
         } else {
             this.error.alasan = 'Silahkan memilih alasan'
         }



        //  masukkan data kedalam suatu body
        
        const body = {
            nama: this.form.name,
            nik: this.form.nik,
            nkk: this.form.nkk,
            photo_ktp: this.form.ktp,
            photo_kk: this.form.kk,
            umur: this.form.umur,
            jenis_kelamin: this.form.jenis_kelamin == 'P' ? 'Perempuan' : 'Laki-laki',
            alamat: this.form.alamat,
            rt: this.form.rt,
            rw: this.form.rw,
            penghasilan_sebelum_pandemi: this.form.beforePandemi,
            penghasilan_setelah_pandemi: this.form.afterPandemi,
            alasan: this.form.alasan == 4 ? this.lainnya : this.form.alasan == 3 ? 'Tergolong fakir/miskin semenjak sebelum Covid' : this.form.alasan == 2 ? 'Kepala Keluarga terdampak atau korban Covid' : 'Kehilangan Pekerjaan' 
        }
        this.setAllToBody(body)
        event.preventDefault()
        
        // alert(JSON.stringify(this.form))
      },
      setAllToBody(item) {
        //   nilai random 
          const random = Math.random() * 1000 + 1000
          setTimeout(()=> {
              let title, message
              if(random < 1500) {
                  title = 'Success'
                  message = 'Data has been send'
                  console.log(item)
              } else {
                  title = 'Failed'
                  message= 'Internal Server Error '
              }
              this.$bvModal.msgBoxOk(message, {
                title,
                size: 'sm',
                buttonSize: 'sm',
                okVariant: 'success',
                headerClass: 'p-2 border-bottom-0',
                footerClass: 'p-2 border-top-0',
                centered: true
                })
                .then(() => {
                    
                })
                .catch(() => {
                    // An error occurred
                })
          }, 1500)
      },
      onReset(event) {
        event.preventDefault()
        // Reset our form values
        this.clearData()
      },
      clearData() {
        this.form.name = ''
        this.form.check = false
        this.form.nik = ''
        this.form.nkk = ''
        this.form.alamat = ''
        this.form.alasan = ''
        this.form.rt = ''
        this.form.rw = ''
        this.form.kk = null
        this.form.ktp = ''
        this.form.beforePandemi = 0
        this.form. afterPandemi = 0
        this.form.jenis_kelamin = 'P'
      }
    }
}
</script>
<style >
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}

/* Firefox */
input[type=number] {
  -moz-appearance: textfield;
}

.ft-12 {
    font-size: 12px;
}
</style>