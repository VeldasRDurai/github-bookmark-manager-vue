<template>
    <b-card className="text-center" header-tag="header" footer-tag="footer">
        <template #header>
            <h3>{{heading}}</h3>
        </template>
        <slot></slot>
        <template #footer>
        </template>
  </b-card>
</template>

<script>
    export default {
        name:'Wrapper',
        props:[ 'heading' ]
    }
</script>