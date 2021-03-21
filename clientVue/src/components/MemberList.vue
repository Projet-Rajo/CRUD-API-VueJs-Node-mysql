<template>
  <div>
    <Row>
      <Table class="table table-bordered table-striped table-condensed">
        <thead>
          <tr>
            <th>ID</th>
            <th>Last Name</th>
            <th>First Name</th>
            <th>Email</th>
            <th colSpan="2">Actions</th>
          </tr>
        </thead>
        <tbody>
          <Member
            v-for="member in memberList"
            v-bind:key="member.id"
            :member="member"
            @onDelete="onDelete"
            @onEdit="onEdit"
          />
        </tbody>
      </Table>
    </Row>
  </div>
</template>

<script>
import Member from "./Member";

export default {
  name: "MemberList",
  components: {
    Member,
  },
  props: {
    memberList: {
      type: Array,
    },
  },
  methods: {
    onDelete(id) {
      // console.log("Member list deleted", id);
      this.$emit("onDeleteApp", id);
    },
    onEdit(data) {
      //console.log("Member list onEdit", data);
      this.$emit("onEdit", data);
    },
  },
};
</script>

<style>
</style>