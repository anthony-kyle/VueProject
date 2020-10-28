<template>
<div class="add">
  <Form :model="new_car" :label-width="80">
    <FormItem label="Brand">
      <Input v-model="new_car.brand" />
    </FormItem>
    <FormItem label="Model">
      <Input v-model="new_car.model" />
    </FormItem>
    <FormItem label="Engine">
      <Input v-model="new_car.engine" />
    </FormItem>
    <FormItem label="Gearbox">
      <Input v-model="new_car.gearbox" />
    </FormItem>
    <Button type="primary" @click="add">Save Car</Button>
  </Form>
</div>
</template>

<script>
// @ is an alias to /src
const apiUrl = 'https://pilcrowmicro.com/api/v1/cars'

export default {
  name: 'add',
  data() {
    return {
      new_car: {},
      err_msg: ''
    }
  },
  methods: {
    add() {
      if (
        this.new_car.brand &&
        this.new_car.model &&
        this.new_car.engine &&
        this.new_car.gearbox
      ) {
        axios
          .post(apiUrl, this.new_car)
          .then(res => {
            if (res.data[0]) {
              this.$router.push('/');
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
          content: 'You need to fill in all fields to save a new car.',
          duration: 0,
          closable: true
        })
      }
    },
  }
}
</script>

<style lang="scss" scoped>
.add {
  padding: 1em;
}
</style>
