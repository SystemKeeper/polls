<!--
  - @copyright Copyright (c) 2018 René Gieling <github@dartcafe.de>
  -
  - @author René Gieling <github@dartcafe.de>
  -
  - @license GNU AGPL version 3 or any later version
  -
  - This program is free software: you can redistribute it and/or modify
  - it under the terms of the GNU Affero General Public License as
  - published by the Free Software Foundation, either version 3 of the
  - License, or (at your option) any later version.
  -
  - This program is distributed in the hope that it will be useful,
  - but WITHOUT ANY WARRANTY; without even the implied warranty of
  - MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
  - GNU Affero General Public License for more details.
  -
  - You should have received a copy of the GNU Affero General Public License
  - along with this program.  If not, see <http://www.gnu.org/licenses/>.
  -
  -->

<template>
	<h2 class="poll-title">
		{{ poll.title }}
		<span v-if="expired" class="label error">{{ t('polls', 'Expired since %n', 1, moment.unix(poll.expire).format('LLLL')) }}</span>
		<span v-if="!expired && poll.expire" class="label success">{{ t('polls', 'Place your votes until %n', 1, moment.unix(poll.expire).format('LLLL')) }}</span>
		<span v-if="poll.deleted" class="label error">{{ t('polls', 'Deleted') }}</span>
	</h2>
</template>

<script>
import { mapState, mapGetters } from 'vuex'

export default {
	name: 'PollTitle',

	computed: {
		...mapState({
			poll: state => state.poll
		}),

		...mapGetters([
			'expired'
		])

	}

}
</script>

<style lang="scss" scoped>
	.pollTitle {
		margin: 8px 0;
	}
</style>
