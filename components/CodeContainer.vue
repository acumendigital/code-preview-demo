<template>
  <div :id="id" class="code__ctn">
    <div class="code__bar">
      <div>{{ codeTitle }}</div>
      <div class="actions">
        <!-- <button @click="editableDark = !editableDark">
          dark
        </button> -->
        <button @click="copyCode">
          <svg width="18" height="18" viewBox="0 0 18 18" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path fill-rule="evenodd" clip-rule="evenodd" d="M8.25 7.5C7.83579 7.5 7.5 7.83579 7.5 8.25V15C7.5 15.4142 7.83579 15.75 8.25 15.75H15C15.4142 15.75 15.75 15.4142 15.75 15V8.25C15.75 7.83579 15.4142 7.5 15 7.5H8.25ZM6 8.25C6 7.00736 7.00736 6 8.25 6H15C16.2426 6 17.25 7.00736 17.25 8.25V15C17.25 16.2426 16.2426 17.25 15 17.25H8.25C7.00736 17.25 6 16.2426 6 15V8.25Z" fill="white"/>
            <path fill-rule="evenodd" clip-rule="evenodd" d="M3 2.25C2.80109 2.25 2.61032 2.32902 2.46967 2.46967C2.32902 2.61032 2.25 2.80109 2.25 3V9.75C2.25 9.94891 2.32902 10.1397 2.46967 10.2803C2.61032 10.421 2.80109 10.5 3 10.5H3.75C4.16421 10.5 4.5 10.8358 4.5 11.25C4.5 11.6642 4.16421 12 3.75 12H3C2.40326 12 1.83097 11.7629 1.40901 11.341C0.987053 10.919 0.75 10.3467 0.75 9.75V3C0.75 2.40326 0.987053 1.83097 1.40901 1.40901C1.83097 0.987053 2.40326 0.75 3 0.75H9.75C10.3467 0.75 10.919 0.987053 11.341 1.40901C11.7629 1.83097 12 2.40326 12 3V3.75C12 4.16421 11.6642 4.5 11.25 4.5C10.8358 4.5 10.5 4.16421 10.5 3.75V3C10.5 2.80109 10.421 2.61032 10.2803 2.46967C10.1397 2.32902 9.94891 2.25 9.75 2.25H3Z" fill="white"/>
          </svg>
        </button>
        <div v-show="codeCopied">
          copied!
        </div>
      </div>
    </div>
    <textarea id="code-preview-ctn" v-model="editableContent" readonly class="inner" rows="5" />
  </div>
</template>

<script>
import CodeMirror from 'codemirror'
import 'codemirror/lib/codemirror.css'
import 'codemirror/theme/material.css'
import 'codemirror/theme/yeti.css'
import 'codemirror/mode/javascript/javascript'
import 'codemirror/mode/php/php'
import 'codemirror/mode/go/go'
import 'codemirror/mode/dart/dart'
import 'codemirror/mode/shell/shell'

export default {
  name: 'CodeContainer',
  props: {
    content: {
      type: String,
      default: () => '// code starts here'
    },
    language: {
      type: String,
      default: () => 'javascript'
    },
    codeTitle: {
      type: String,
      default: () => 'Code Title'
    },
    dark: {
      type: Boolean,
      default: () => true
    },
    id: {
      type: String,
      default: 'js1'
    }
  },
  data () {
    return {
      editableContent: this.content,
      editableDark: this.dark,
      cm: null,
      codeCopied: false
    }
  },
  watch: {
    editableDark: {
      handler (_val, _oldVal) {
        this.initializeCodeMirror()
      }
    }
  },
  mounted () {
    this.initializeCodeMirror()
  },
  methods: {
    initializeCodeMirror () {
      this.cm = CodeMirror.fromTextArea(document.querySelector(`#${this.id} > .inner`), {
        mode: this.language,
        theme: this.dark ? 'material' : 'yeti',
        readOnly: true
      })
    },
    copyCode () {
      const codeContainer = document.querySelector('.code__ctn .CodeMirror-code')
      const newElement = document.createElement('textarea')
      newElement.value = codeContainer.innerText
      document.body.appendChild(newElement)
      newElement.select()
      document.execCommand('copy')
      document.body.removeChild(newElement)
      this.codeCopied = true
      setTimeout(() => { this.codeCopied = false }, 3000)
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto+Mono&display=swap');
.code__ctn {
  border-radius: 8px;
  font-family: inherit;
  margin-bottom: 12px;
}
.code__bar {
  background-color: #476BD2;
  font-size: 0.95rem;
  color: #FFFFFF;
  padding: 0 16px;
  height: 40px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-top-right-radius: 8px;
  border-top-left-radius: 8px;
}
.code__bar .actions {
  font-family: 'Material Icons';
}
.code__bar button {
  font-family: 'Material Icons';
  font-size: 1rem;
  height: 32px;
  width: 32px;
  border-radius: 16px;
  border: none;
  background: transparent;
  display: grid;
  place-items: center;
}
.code__bar button:hover {
  background: #0000002a;
}
.CodeMirror {
  height: auto;
  padding: 16px;
  padding-top: 0;
  border-bottom-right-radius: 8px;
  border-bottom-left-radius: 8px;
}
.code__ctn pre {
  margin-left: 32px;
}
.code__ctn span {
  font-family: 'Roboto Mono', monospace  !important;
  font-size: 0.775rem;
  line-height: 1.5rem;
}
</style>
