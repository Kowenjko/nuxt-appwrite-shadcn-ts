<script setup lang="ts">
import { COLLECTION_DEALS, DB_ID } from '@/app.constants'
import { KANBAN_DATA } from '@/components/kanban/kanban.data'
import type { Card, Column } from '@/components/kanban/kanban.types'
// import { DB } from '@/utils/appwrite'
// import { useMutation, useQuery } from '@tanstack/vue-query'
import { ref } from 'vue'
import type { EnumStatus, IDeal } from '~/types/deals.types'

useSeoMeta({
	title: 'Home',
})

let board = ref<Column[]>(KANBAN_DATA)

const dragCard = ref<Card | null>(null)
const sourceColumn = ref<Column | null>(null)

// const { data, suspense, isSuccess, refetch } = useQuery({
// 	queryKey: ['deals'],
// 	queryFn: () => DB.listDocuments(DB_ID, COLLECTION_DEALS, []),
// 	select: (data) => {
// 		const boardValue = board.value
// 		const columnsMap = new Map(
// 			boardValue.map((column) => [
// 				column.id,
// 				{
// 					...column,
// 				},
// 			])
// 		)
// 		const docs = data.documents as unknown as IDeal[]

// 		docs.forEach((deal) => {
// 			if (columnsMap.has(deal.status)) {
// 				const column = columnsMap?.get(deal.status)
// 				if (column) {
// 					column.items.push({
// 						id: deal.$id,
// 						content: deal.name,
// 						// TODO: Add fields
// 					})
// 				}
// 			}
// 		})

// 		return Array.from(columnsMap.values())
// 	},
// })

// await suspense()

// const { mutate } = useMutation({
// 	mutationKey: ['move card'],
// 	mutationFn: (docId: string, status?: EnumStatus) =>
// 		DB.updateDocument(DB_ID, COLLECTION_DEALS, docId, {
// 			status,
// 		}),
// 	onSuccess: () => {
// 		refetch()
// 	},
// })

function handleDragStart(card: Card, column: Column) {
	dragCard.value = card
	sourceColumn.value = column
}

function handleDragOver(event: DragEvent) {
	event.preventDefault()
}

// TODO: LIST FULL
/*
	- Deals
	- Open deals modal
	- Comments write
	- Customers page
	- ?FiltersDeals
*/

function handleDrop(targetColumn: Column) {
	// if (dragCard.value && sourceColumn.value) {
	// 	console.log('test')
	// 	// TODO: Mutate when drop
	// 	// mutate(dragCard.value.id, targetColumn.id.toString())
	// }
	// //add
	// targetColumn.items.push(dragCard.value)
	// //remove
	// const index = sourceColumn.value.items.findIndex(
	// 	(card) => card.id === dragCard.value?.id
	// )
	// if (index > -1) {
	// 	sourceColumn.value.items.splice(index, 1)
	// }
	// dragCard.value = null
	// sourceColumn.value = null
}
</script>

<template>
	<div class="p-10">
		<h1 class="font-bold text-2xl mb-10">Kanban Board</h1>
		<div class="card-scene">
			<ClientOnly>
				<div class="grid grid-cols-5 gap-20">
					<div
						v-for="column in KANBAN_DATA"
						:key="column.id"
						@dragover="handleDragOver"
						@drop="() => handleDrop(column)"
					>
						<div class="rounded bg-slate-700 py-1 px-5 mb-5">
							{{ column.name }}
						</div>
						<div>
							<Card
								v-for="card in column.items"
								:key="card.id"
								class="mb-3"
								draggable="true"
								@dragstart="() => handleDragStart(card, column)"
							>
								<CardHeader>
									<CardTitle>{{ card.id }}</CardTitle>
									<CardDescription>UiCard Description</CardDescription>
								</CardHeader>
								<CardContent>
									{{ card.content }}
								</CardContent>
								<CardFooter> UiCard Footer </CardFooter>
							</Card>
						</div>
					</div>
				</div>
			</ClientOnly>
		</div>
	</div>
</template>
