<template>
  <transition>
    <v-container>
      <v-form>
        <v-layout align-content-start="">
          <v-flex xs3>
            <v-text-field name="selectedQuote" label="Quote" v-model="stockForm.selectedQuote"></v-text-field>
          </v-flex>
          <v-spacer></v-spacer>
          <v-flex xs3>
            <v-text-field v-model.number="stockForm.quantity" label="Quantity" id="id"></v-text-field>
          </v-flex>
          <v-spacer></v-spacer>
          <v-flex xs3>
            <v-text-field name="price" label="Price" id="Price"></v-text-field>
          </v-flex>

        </v-layout>
        <v-layout>
          <v-flex xs3>
           <v-menu
             ref="menuRef"
             lazy
             :close-on-content-click="false"
             v-model="menuValue"
             transition="scale-transition"
             offset-y
             full-width
             :nudge-right="40"
             min-width="290px"
             :return-value.sync="datePickerValue"
           >
             <v-text-field
               slot="activator"
               label="label"
               v-model="datePickerValue"
               prepend-icon="event"
               readonly
             ></v-text-field>
               <v-date-picker v-model="datePickerValue" no-title scrollable>
                 <v-spacer></v-spacer>
                 <v-btn flat color="primary" @click="menuValue = false">Cancel</v-btn>
                 <v-btn flat color="primary" @click="$refs.menuRef.save(date)">OK</v-btn>
               </v-date-picker>
           </v-menu>
           </v-flex>
          <v-spacer></v-spacer>
          <v-flex xs3>

          </v-flex>
          <v-spacer></v-spacer>
          <v-flex xs3></v-flex>
          <v-spacer></v-spacer>
        </v-layout>
      </v-form>

    </v-container>
  </transition>


</template>
<script>
  import FileUpload from "vue-upload-component";
  export default {
    props: {},
    data() {
      return {
        quotes: [],
        selectedQuote: "myQuote",
        stockForm: {},
        sample: "srinivas",
        files: [],
        files: [],
        accept: "image/png,image/gif,image/jpeg,image/webp",
        extensions: "gif,jpg,jpeg,png,webp",
        // extensions: ['gif', 'jpg', 'jpeg','png', 'webp'],
        // extensions: /\.(gif|jpe?g|png|webp)$/i,
        minSize: 1024,
        size: 1024 * 1024 * 10,
        multiple: true,
        directory: false,
        drop: true,
        dropDirectory: true,
        addIndex: false,
        thread: 3,
        name: "file",
        postAction: "/upload/post",
        putAction: "/upload/put",
        headers: {
          "X-Csrf-Token": "xxxx"
        },
        data: {
          _csrf_token: "xxxxxx"
        },
        autoCompress: 1024 * 1024,
        uploadAuto: false,
        isOption: false,
        addData: {
          show: false,
          name: "",
          type: "",
          content: ""
        },
        editFile: {
          show: false,
          name: ""
        }
      };
    },

    components: {
      FileUpload
    },
    methods: {
      addStock() {
        console.log(this.stockForm);
      },
      inputFilter(newFile, oldFile, prevent) {
        if (newFile && !oldFile) {
          // Before adding a file
          // 添加文件前
          // Filter system files or hide files
          // 过滤系统文件 和隐藏文件
          if (/(\/|^)(Thumbs\.db|desktop\.ini|\..+)$/.test(newFile.name)) {
            return prevent();
          }
          // Filter php html js file
          // 过滤 php html js 文件
          if (/\.(php5?|html?|jsx?)$/i.test(newFile.name)) {
            return prevent();
          }
        }
      },
      inputFile(newFile, oldFile) {
        if (newFile && !oldFile) {
          // add
          newFile.blob = "";
          let URL = window.URL || window.webkitURL;
          if (URL && URL.createObjectURL) {
            newFile.blob = URL.createObjectURL(newFile.file);
          }
        }
        if (newFile && oldFile) {
          // update
          console.log("update", newFile);
        }
        if (!newFile && oldFile) {
          // remove
          console.log("remove", oldFile);
        }
      }
    }
  };

</script>
<style lang="less">
  .file-uploads.file-uploads-html5 input[type="file"] {
    position: relative !important;
    border: 1px solid black;
    width: 100%;
    height: 100px;
  }

  .padding-x-no {
    padding-left: 0;
    padding-right: 0;
  }

  .files-drop {
    min-height: 80px;
    height: auto;
    text-align: center;
    vertical-align: middle;
    margin: 0 auto;
    border: 1px solid grey;
    border-radius: 2px;
    &:hover {
      background-color: rgb(250, 248, 248);
    }
  }

  .dropdown-toggle.file-uploads {
    display: none;
  }

</style>
