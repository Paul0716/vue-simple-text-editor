<template>
    <div class="simple-text-editor">
        <!-- button-group -->
        <div id="button-group"
            :class="{ 'hide': !editable }"
            class="button-group"
            ref="buttonGroup">
            <button>Bold</button>
            <button>Italic</button>
            <button>Underline</button>
        </div>

        <div
            @click.prevent.stop="toggleEdit()"
            v-html="text"
            :class="{'text-editable': editable}"
            :contenteditable="editable">

        </div>
    </div>
    

</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';

@Component
export default class SimpleTextEditor extends Vue {
    editable: boolean = false;
    text: string = "demo";

    toggleEdit() {
        this.editable = !this.editable;
    }

    mounted(): void {
        const rootEl = document.getElementsByClassName('simple-text-editor')[0] as HTMLElement;
        rootEl.addEventListener('mouseup', this.getSelectedText);
    }

    getSelectedText(ev: MouseEvent): void {
        const selected = window.getSelection();
        const oRange = selected.getRangeAt(0); //get the text range
        const oRect = oRange.getBoundingClientRect();
        
        // const buttonGroup = document.querySelector('#button-group') as HTMLElement;
        const buttonGroup = this.$refs.buttonGroup as HTMLElement;
        // console.log(buttonGroup);
        buttonGroup.style.top = `${oRect.top - oRect.height}px`;
        buttonGroup.style.left = `${oRect.left - oRect.width/2}px`;
        // console.log(oRange, oRect);
        
    }

}
</script>

<style lang="scss" scoped>
    .button-group {
        position:fixed;
        opacity: 1;
        transition: opacity .3s ease-in-out;
    }
    .text-editable {
        border: 1px solid #8c8c8c;
    }
    .hide {
        opacity: 0;
        
    }
</style>
