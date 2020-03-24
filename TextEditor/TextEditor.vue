<template>
    <section>
        <quill-editor 
		v-if="show" 
		v-model="texto"  
		@input="onTextChange"
		:options="editorOption"></quill-editor>
    </section>
</template>
<script>
import 'quill/dist/quill.core.css' // import styles
import 'quill/dist/quill.snow.css' // for snow theme
import 'quill/dist/quill.bubble.css' // for bubble theme

export default {
    props:['toolbarText','toolbarVideo','toolbarImage','toolbarLink','imagePaste','imageDrop','placeholder','value'],
    data(){
        return{
			show:false,
            texto:  this.value,
            editorOption: {
                placeholder: this.placeholder != undefined ? this.placeholder : "Inserte el texto aquí..",
                modules: {
                    imageDrop: this.imageDrop != undefined ? this.imagePaste: true,
                    imagePaste: this.imagePaste != undefined ? this.imagePaste: true,
                    toolbar: [
                        !this.toolbarText ? [] :["bold", "italic", "underline", "strike"],
                        !this.toolbarText ? [] :["blockquote", "code-block"],
                        !this.toolbarText ? [] :[{ header: 1 }, { header: 2 }],
                        !this.toolbarText ? [] :[{ list: "ordered" }, { list: "bullet" }],
                        !this.toolbarText ? [] :[{ script: "sub" }, { script: "super" }],
                        !this.toolbarText ? [] :[{ indent: "-1" }, { indent: "+1" }],
                        !this.toolbarText ? [] :[{ direction: "rtl" }],
                        !this.toolbarText ? [] :[{ size: ["small", false, "large", "huge"] }],
                        !this.toolbarText ? [] :[{ header: [1, 2, 3, 4, 5, 6, false] }],
                        !this.toolbarText ? [] :[{ font: [] }],
                        !this.toolbarText ? [] :[{ color: [] }, { background: [] }],
                        !this.toolbarText ? [] :[{ align: [] }],
                        !this.toolbarText ? [] :["clean"],
                        [this.toolbarLink ? "link" : '',this.toolbarImage ? "image" : '', this.toolbarVideo? "video": ''],
                       
                    ],
                    imageResize: {
                        displayStyles: {
                            backgroundColor: "black",
                            border: "none",
                            color: "white"
                        },
                        modules: [ "Toolbar","Resize","DisplaySize"] // ,
                    }
                }
            }
        };
	},
	mounted(){
		this.show=true;
	},
	methods:{
		onTextChange(event){
			
			this.$emit('input', this.texto)
		}
	}
}
</script>
<style scoped>
.ql-stroke {
  stroke: #4f748e;
  fill: transparent;
  stroke-linecap: round;
  stroke-linejoin: round;
  stroke-width: 1.5px;
}

.ql-stroke-active {
  stroke: #333;
  fill: transparent;
  stroke-linecap: round;
  stroke-linejoin: round;
  stroke-width: 2px;
}

.ql-stroke-mitter {
  stroke: #4f748e;
  fill: transparent;
}

.ql-stroke-mitter-active {
  stroke: #333;
  fill: transparent;
}

.ql-fill {
  fill: #4f748e;
}

.ql-fill-active {
  fill: #333;
}

.ql-even {
  stroke: #4f748e;
  fill: #fff;
}

.ql-even-active {
  stroke: #333;
  fill: #fff;
}

/*
  .ql-color-label {
    fill: red;
  }
*/

.ql-transparent {
  opacity: 0.2;
}

.ql-thin {
  stroke: #4f748e;
  fill: transparent;
  stroke-width: 1;
}

.ql-thin-active {
  stroke: #333;
  fill: transparent;
  stroke-width: 2;
}

.toolbar-item {
  width: 25px;
  height: 25px;
  margin: 5px;
}

.toolbar-item-active {
  width: 25px;
  height: 25px;
  margin: 4px;
  border: 1px solid #2e4453;
}

.toolbar-select {
  display: inline-block;
  margin-right: 3px;
}

.editor {
  padding: 5px;
  margin: 5px 10px 5px 5px;
  border: 1px solid #2e4453;
}

.toolbar-item-disable > * {
  stroke: #ccc;
  cursor: not-allowed;
}
</style>