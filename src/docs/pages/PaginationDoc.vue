<template>
  <section class="container-fluid">
    <div class="row">
      <div class="col-xs-12">
        <anchor-header text="Pagination" source-folder="pagination"></anchor-header>
      </div>
    </div>
    <div class="row">
      <div class="col-xs-12">
        <div>
          <pagination :boundary-links="boundaryLinks"
                      :direction-links="directionLinks"
                      :total-page="totalSize"
                      :size="size"
                      v-model="currentPage"
                      @page-changed="changePage"
                      :max-size="maxSize"></pagination>
        </div>
        <div class="well">
          <form class="form-horizontal">
            <div class="form-group">
              <div class="col-xs-12">
                <label class="checkbox-inline">
                  <input v-model="boundaryLinks" type="checkbox"> Boundary Links
                </label>
                <label class="checkbox-inline">
                  <input v-model="directionLinks" type="checkbox"> Direction Links
                </label>
              </div>
            </div>
            <div class="form-group">
              <div class="col-md-6">
                <label>Current Page:</label>
                <div class="input-group">
                  <input class="form-control" step="1" min="1" :max="totalSize" v-model.number="currentPage"
                         type="number">
                  <span class="input-group-addon" v-text="'/ '+totalSize"></span>
                </div>
              </div>
              <div class="col-md-6">
                <label>Size:</label>
                <select class="form-control" v-model="size">
                  <option value="sm">sm</option>
                  <option value="">md</option>
                  <option value="lg">lg</option>
                </select>
              </div>
            </div>
            <div class="form-group">
              <div class="col-md-6">
                <label>Total Page:</label>
                <input class="form-control" step="1" min="0" v-model.number="totalSize" type="number">
              </div>
              <div class="col-md-6">
                <label>Max Size:</label>
                <input class="form-control" step="1" min="0" v-model.number="maxSize" type="number">
              </div>
            </div>
          </form>
        </div>
      </div>
    </div>
    <div class="row">
      <div class="col-xs-12">
        <demo-code-panel demo-file="PaginationDoc.vue">
        <pre><code>
&lt;pagination v-model=&quot;currentPage&quot; :total-page=&quot;totalSize&quot; :max-size=&quot;maxSize&quot;&gt;&lt;/pagination&gt;
        </code></pre>
        </demo-code-panel>
        <api-panel :api="api" folder="pagination" file="Pagination.vue"></api-panel>
      </div>
    </div>
  </section>
</template>

<script>
  import AnchorHeader from '../architecture/AnchorHeader.vue'
  import DemoCodePanel from '../architecture/DemoCodePanel.vue'
  import Pagination from '../../components/pagination/Pagination.vue'
  import hljsMixin from './../mixins/hljsMixin'
  import ApiPanel from './../architecture/ApiPanel.vue'
  export default {
    mixins: [hljsMixin],
    components: {AnchorHeader, DemoCodePanel, Pagination, ApiPanel},
    data () {
      return {
        api: {
          props: [
            {
              name: 'v-model',
              required: true,
              desc: 'The current page',
              type: 'Number',
              'default': ''
            },
            {
              name: 'boundary-links',
              desc: 'Whether to display First / Last buttons',
              type: 'Boolean',
              'default': 'false'
            },
            {
              name: 'direction-links',
              desc: 'Whether to display Previous / Next buttons',
              type: 'Boolean',
              'default': 'true'
            },
            {
              name: 'total-page',
              required: true,
              desc: 'Total number of pages',
              type: 'Number',
              'default': ''
            },
            {
              name: 'max-size',
              desc: 'Maximum number of pages per chunk',
              type: 'Number',
              'default': '5'
            },
            {
              name: 'size',
              desc: 'String',
              type: 'The pagination size. Support: sm / md / lg',
              'default': 'md'
            }
          ],
          events: [
            {
              name: 'page-changed',
              params: ['index'],
              desc: 'Fire after page changed, with the index number changed to'
            }
          ]
        },
        totalSize: 18,
        maxSize: 5,
        currentPage: 1,
        boundaryLinks: true,
        directionLinks: true,
        size: ''
      }
    },
    methods: {
      changePage () {
        console.log('Page is changed!')
      }
    }
  }
</script>

<style lang="less" rel="stylesheet/less" scoped>

</style>
