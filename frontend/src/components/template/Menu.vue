<template>
  <aside class="menu" v-show="isMenuVisible">
      <div class="menu-filter">
          <i class="fa fa-search fa-lg"></i>
          <input type="text" v-model="treeFilter" class="filter-field" placeholder="Digite para filtrar...">
      </div>
      <Tree :data="treeData" :options="treeOptions" :filter="treeFilter" ref="tree"></Tree>
  </aside>
</template>

<script>
import { mapState } from 'vuex'
import Tree from 'liquor-tree'
import { baseApiUrl } from '@/global'
import axios from 'axios'

export default {
    name: 'Menu',
    components: { Tree },
    computed: mapState(['isMenuVisible']),
    data(){
        return {
            treeFilter: '',
            treeData: this.getTreeData(),
            treeOptions: {
                propertyNames:{ 'text': 'name' },
                filter: {
                    emptyText: 'Categoria não encontrada'
                }
            }
        }
    },
    methods: {
        getTreeData(){
            const url = `${baseApiUrl}/categories/tree`
            return axios.get(url).then(res => res.data)
        },
        onNodeSelect(node){
            this.$router.push({
                name: 'articlesByCategory',
                params: { id: node.id }
            })

            if(this.$mq === 'xs' || this.$mq === 'sm'){
                this.$store.commit('toggleMenu', false)
            }
        }
    },
    mounted(){
        this.$refs.tree.$on('node:selected', this.onNodeSelect)
    }
}
</script>

<style>
    .menu{
        grid-area: menu;
        background: white;

        display: flex;
        flex-direction: column;
        flex-wrap: wrap;
    }

    .menu a,
    .menu a:hover {
        color: #424242;
        text-decoration: none;
    }

    .menu .tree-node.selected > .tree-content,
    .menu .tree-node .tree-content:hover {
        background-color: rgba(0, 0, 0, 0.1);
    }
    
    .menu .menu-filter {
        display: flex;
        justify-content: center;
        align-items: center;
        margin: 20px;
        padding-bottom: 8px;
        border-bottom: 1px solid #AAA;
    }
    .menu .menu-filter i {
        color: #424242;
        margin-right: 10px;
    }
    .menu input {
        color: #424242;
        font-size: 1.3rem;
        border: 0;
        outline: 0;
        width: 100%;
        background: transparent;
    }
    .tree-filter-empty {
        color: #424242;
        font-size: 1.2rem;
        margin-left: 20px;
    }
</style>