<template></template>
<script>
export default {
  data() {
    return {
      crudId: this.$uid()
    }
  },
  computed: {
    crudData() {
      return {
        crudId: this.crudId,
        entityName: config("main.qrequestable.entityNames.status"),
        apiRoute: 'apiRoutes.qrequestable.statuses',
        permission: 'requestable.requestables',
        extraFormFields: 'requestable.crud-fields.status',
        create: {
          title: this.$tr('qrequestable.layout.newStatus')
        },
        read: {
          showAs: (config('app.mode') == 'iadmin') ? 'table' : 'grid',
          columns: [
            {name: 'id', label: this.$tr('ui.form.id'), field: 'id', sortable: true, align: 'left'},
            {name: 'title', label: this.$tr('ui.form.title'), field: 'title', align: 'left', sortable: true},
            {name: 'value', label: this.$tr('ui.label.value'), field: 'value', align: 'left', sortable: true},
            {
              name: 'category', label: this.$tr('ui.form.category'),
              align: 'left', field: 'category', sortable: true,
              format: val => ((val && val.title) ? val.title : '-')
            },
            {
              name: 'createdAt', label: this.$tr('ui.form.createdAt'), field: 'createdAt',
              format: val => val ? this.$trd(val) : '-',
              align: 'left', sortable: true
            },
            {
              name: 'actions', label: this.$tr('ui.form.actions'), align: 'center'
            }
          ],
          requestParams: {
            include: 'category'
          },
          filters: {
            categoryId: {
              value: null,
              type: 'select',
              props: {
                label: `${this.$tr('ui.form.category')}`,
                clearable: true
              },
              loadOptions: {
                apiRoute: 'apiRoutes.qrequestable.categories'
              }
            }
          }
        },
        update: {
          title: this.$tr('qrequestable.layout.updateStatus'),
          requestParams: {include: 'category'}
        },
        delete: false,
        formLeft: {
          id: {value: ''},
          title: {
            value: '',
            type: 'input',
            isTranslatable: true,
            props: {
              label: `${this.$tr('ui.form.title')}*`,
              rules: [
                val => !!val || this.$tr('ui.message.fieldRequired')
              ],
            },
          },
          value: {
            value: '',
            type: 'input',
            props: {
              type: 'number',
              label: `${this.$tr('ui.label.value')}*`,
              rules: [
                val => !!val || this.$tr('ui.message.fieldRequired')
              ],
            },
          },
          categoryId: {
            value: null,
            type: 'select',
            props: {
              label: `${this.$tr('ui.form.category')}`
            },
            loadOptions: {
              apiRoute: 'apiRoutes.qrequestable.categories'
            }
          }
        },
      }
    },
    //Crud info
    crudInfo() {
      return this.$store.state.qcrudComponent.component[this.crudId] || {}
    }
  },
  methods: {}
}
</script>
