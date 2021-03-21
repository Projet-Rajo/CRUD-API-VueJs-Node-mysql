<template>
  <tr>
    <td>{{ member.id }}</td>
    <td>{{ member.lastName }}</td>
    <td>{{ member.firstName }}</td>
    <td>{{ member.email }}</td>
    <td>
      <Button class="btn btn-info" @click="onEdit">Edit</Button>
    &nbsp;
      <Button class="btn btn-danger" @click="onDel">Delete</Button>
    </td>
  </tr>
</template>

<script>
export default {
  name: "Member",
  props: {
    member : {
      type: Object
    }
  },
  methods: {
    onDel(){
      // console.log("Member deleted "+this.member.id);
      this.$emit("onDelete", this.member.id);
    },
    onEdit(){
      // console.log("Member deleted "+this.member.id);
      this.$emit("onEdit", this.member);
    }
  }
};
</script>

<style>
</style>