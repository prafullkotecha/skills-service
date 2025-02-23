/*
Copyright 2020 SkillTree

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    https://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
*/
<template>
  <div class="row">
    <div class="col-auto">
      <b-button
        :to="{ name:'SubjectSkills', params: { projectId: this.subject.projectId, subjectId: this.subject.subjectId, subject: this.subject}}"
        variant="outline-primary" size="sm" class="mr-2"
        :aria-label="`Manage subject ${subject.name}`"
        :data-cy="`subjCard_${subject.subjectId}_manageBtn`">
        Manage <i class="fas fa-arrow-circle-right" aria-hidden="true"/>
      </b-button>
    </div>

    <div class="col text-right">
      <b-button-group size="sm" class="buttons mr-2">
        <b-button ref="editBtn"
                  size="sm"
                  variant="outline-primary"
                  @click="$emit('edit-subject')"
                  title="Edit Project"
                  data-cy="editSubjBtn"><i class="fas fa-edit" aria-hidden="true"/></b-button>

        <span v-b-tooltip.hover="deleteDisabledText">
          <b-button variant="outline-primary"
                    class="last-right-group-btn"
                    size="sm"
                    @click="$emit('delete-subject')"
                    :disabled="isDeleteDisabled"
                    title="Delete Project"
                    data-cy="deleteSubjBtn"><i class="text-warning fas fa-trash" aria-hidden="true"/></b-button>
        </span>
      </b-button-group>

      <b-button-group size="sm" class="buttons">
        <b-button variant="outline-primary"
                  @click="$emit('move-up-subject')"
                  :disabled="subject.isFirst"
                  title="Sort Order - Move up"
                  data-cy="moveSubjUpBtn"><i class="fas fa-arrow-circle-up text-info" aria-hidden="true"/></b-button>
        <b-button variant="outline-primary"
                  @click="$emit('move-down-subject')"
                  :disabled="subject.isLast"
                  title="Sort Order - Move down"
                  data-cy="moveSubjDownBtn"><i class="fas fa-arrow-circle-down text-info" aria-hidden="true"/>
        </b-button>
      </b-button-group>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'SubjectCardControls',
    props: {
      subject: Object,
      isDeleteDisabled: Boolean,
      deleteDisabledText: String,
    },
    methods: {
      focusOnEdit() {
        this.$refs.editBtn.focus();
      },
    },
  };
</script>

<style scoped>
.last-right-group-btn {
  border-top-left-radius: 0;
  border-bottom-left-radius: 0;
  border-left: none;
}
</style>
