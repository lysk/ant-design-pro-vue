<script>
  import { mapState } from "vuex"
  import { colorList } from '@/components/tools/setting'
  import ASwitch from 'ant-design-vue/es/switch'
  import AList from "ant-design-vue/es/list"
  import AListItem from "ant-design-vue/es/list/Item"

  const Meta = AListItem.Meta

  export default {
    components: {
      AListItem,
      AList,
      ASwitch,
      Meta
    },
    data () {
      return {
      }
    },
    computed: {
      ...mapState({
        theme: state => state.app.theme,
        color: state => state.app.color
      })
    },
    filters: {
      themeFilter(theme) {
        const themeMap = {
          'dark': '暗色',
          'light': '白色'
        }
        return themeMap[theme]
      },
    },
    methods: {
      colorFilter(color) {
        const c = colorList.filter(o => o.color === color)[0]
        return c && c.key
      },

      onChange (checked) {
        if (checked) {
          this.$store.dispatch('ToggleTheme',  'dark')
        } else {
          this.$store.dispatch('ToggleTheme',  'light')
        }
      }
    },
    render () {
      return (
        <AList itemLayout="horizontal">
          <AListItem>
            <Meta>
              <a slot="title">风格配色</a>
              <span slot="description">
                整体风格配色设置
              </span>
            </Meta>
            <div slot="actions">
              <ASwitch checkedChildren="暗色" unCheckedChildren="白色" defaultChecked={this.theme === 'dark' && true || false} onChange={this.onChange} />
            </div>
          </AListItem>
          <AListItem>
            <Meta>
              <a slot="title">主题色</a>
              <span slot="description">
                页面风格配色： <a domPropsInnerHTML={ this.colorFilter(this.color) }/>
              </span>
            </Meta>
          </AListItem>
        </AList>
      )
    }
  }
</script>

<style scoped>

</style>