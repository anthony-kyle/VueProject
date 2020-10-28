<template>
<div class="home">
  <Table v-if="!err_msg.length" border stripe :columns="columns" :data="car_list" :no-data-text="notice"></Table>
  <Alert v-else type="error">{{ err_msg }}</Alert>
  <Modal v-model="modal_edit" title="Edit Car Information" @on-ok="edit">
    <Form :model="edit_car" :label-width="60">
      <FormItem label="Brand">
        <Input v-model="edit_car.brand" />
      </FormItem>
      <FormItem label="Model">
        <Input v-model="edit_car.model" />
      </FormItem>
      <FormItem label="Engine">
        <Input v-model="edit_car.engine" />
      </FormItem>
      <FormItem label="Gearbox">
        <Input v-model="edit_car.gearbox" />
      </FormItem>
    </Form>
  </Modal>
</div>
</template>

<script>
// @ is an alias to /src
const apiUrl = 'https://pilcrowmicro.com/api/v1/cars'
export default {
  name: 'Home',
  created() {
    axios
      .get(apiUrl)
      .then(res => {
        this.empty_data()
        if (res.data[0]) {
          if (res.data[1].length) {
            this.car_list = res.data[1]
          } else {
            this.notice = 'No Data Retrieved'
          }
        } else {
          this.err_msg = res.data[1]
        }
      })
      .catch(err => {
        this.empty_data()
        this.err_msg = 'Sorry, AJAX error'
      })
  },
  data() {
    return {
      columns: [{
          title: 'Brand',
          key: 'brand'
        },
        {
          title: 'Model',
          key: 'model'
        },
        {
          title: 'Engine',
          key: 'engine'
        },
        {
          title: 'Gearbox',
          key: 'gearbox'
        },
        {
          title: 'Actions',
          render: (h, params) => {
            return h('div', [
              h('Button', {
                props: {
                  type: 'warning',
                  icon: 'ios-trash'
                },
                on: {
                  click: () => {
                    this.delete(params)
                  }
                }
              }),
              h('Button', {
                props: {
                  type: 'primary',
                  icon: 'ios-create'
                },
                on: {
                  click: () => {
                    this.modal_edit = true
                    this.edit_car = {
                      ...params.row
                    }
                  }
                }
              })
            ])
          }
        }
      ],
      car_list: [],
      edit_car: {},
      notice: '',
      err_msg: '',
      modal: false,
      modal_edit: false
    }
  },
  methods: {
    edit() {
      if (
        this.edit_car.brand &&
        this.edit_car.model &&
        this.edit_car.engine &&
        this.edit_car.gearbox &&
        this.edit_car.id &&
        this.edit_car._index >= 0
      ) {
        axios
          .patch(apiUrl + '/' + this.edit_car.id, this.edit_car)
          .then(res => {
            if (res.data[0]) {
              this.car_list[this.edit_car._index].brand = this.edit_car.brand
              this.car_list[this.edit_car._index].model = this.edit_car.model
              this.car_list[this.edit_car._index].engine = this.edit_car.engine
              this.car_list[
                this.edit_car._index
              ].gearbox = this.edit_car.gearbox
            } else {
              this.$Message.error({
                content: res.data[1],
                duration: 0,
                closable: true
              })
            }
          })
          .catch(err => {
            this.$Message.error({
              content: 'AJAX Error',
              duration: 0,
              closable: true
            })
          })
      } else {
        this.$Message.error({
          content: 'You need to fill in all fields to update a cars details.',
          duration: 0,
          closable: true
        })
      }
    },
    empty_data() {
      this.err_msg = ''
      this.notice = ''
      this.car_list = []
      return true
    },
    cors_update() {
      axios
        .get(apiUrl)
        .then(res => {
          console.log(res.data)
        })
        .catch(err => {
          console.error('Error:', err)
        })
    },
    delete(params) {
      axios
        .delete(apiUrl + '/' + params.row.id)
        .then(res => {
          if (res.data[0]) {
            // console.log('succeed')
            this.car_list.splice(params.index, 1)
          } else {
            // delete failure
            this.$Message.error({
              content: res.data[1],
              duration: 0,
              closable: true
            })
          }
        })
        .catch(err => {
          this.$Message.error({
            content: 'Ajax Error' + err,
            duration: 0,
            closable: true
          })
        })
    }
  }
}
</script>
