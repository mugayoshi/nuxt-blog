<template>
  <section class="container posts-page">
    <el-card>
      <div slot="header" class="clearfix">
        <span>新規投稿</span>
      </div>
      <el-table :data="showPosts" style="width: 100%" class="table">
        <el-table-column prop="title" label="タイトル"> </el-table-column>
        <el-table-column prop="user.id" label="投稿者" width="180">
        </el-table-column>
        <el-table-column prop="created_at" label="投稿日時" width="240">
        </el-table-column>
      </el-table>
    </el-card>
  </section>
</template>

<script>
export default {
    computed: {
        showPosts(){
            return [
                {
                    id: '001',
                    title: 'How to develop Nuxt.js app',
                    body: 'Hello Nuxt.js',
                    created_at: '2020/02/10 12:00:00',
                    user: {
                        id: 'potato4d'
                    }
                },
                {
                    id: '002',
                    title: 'Deploy Nuxt.js app to Heroku',
                    body: 'Heorku is free',
                    created_at: '2020/03/10 12:00:00',
                    user: {
                        id: 'potato4d'
                    }
                }
            ]
        }
    }
}
</script>

<style scoped>
.posts-page .el-table__row {
    cursor: pointer;
}
</style>
