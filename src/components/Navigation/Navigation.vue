<template>
    <nav aria-label="breadcrumb">
      <ol class="breadcrumb">
        <li class="breadcrumb-item" :class="{ active : !showAddPage }" >
          <div @click="$emit('gotoHome')" >Github Bookmark Manager</div>
        </li>
        <li class="breadcrumb-item" :class="{ active : showAddPage }" >
          <div @click="$emit('gotoAddNew')" >Add New</div>
        </li>
      </ol>
    </nav>
</template>

<script>
    export default {
        name:"Navigation",
        props : ['showAddPage', 'handlePathUpdate'],
    }
</script>
<style scoped >
    .breadcrumb-item {
        color: blue;
        cursor: pointer;
    }

    .breadcrumb-item.active {
       cursor: text;
    }
</style>