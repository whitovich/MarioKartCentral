<script lang="ts">
    import Section from "$lib/components/common/Section.svelte";
    import { onMount } from "svelte";
    import type { WordFilter } from "$lib/types/word-filter";
    import Button from "$lib/components/common/buttons/Button.svelte";
    import LL from "$i18n/i18n-svelte";
    import type { UserInfo } from "$lib/types/user-info";
    import { user } from "$lib/stores/stores";
    import { check_permission, permissions } from "$lib/util/permissions";

    let words_text = ""

    let user_info: UserInfo;
    user.subscribe((value) => {
        user_info = value;
    });

    onMount(async () => {
        const res = await fetch(`/api/moderator/wordFilter`);
        if(res.status === 200) {
            const body: WordFilter = await res.json();
            words_text = body.words.toSorted().join("\n");
        }
    });

    async function editFilter() {
        const new_words = words_text.split("\n");
        const payload: WordFilter = {"words": new_words};
        const endpoint = `/api/moderator/wordFilter/edit`;
        const response = await fetch(endpoint, {
            method: 'POST',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify(payload),
        });
        const result = await response.json();
        if (response.status < 300) {
            window.location.reload();
        } else {
            alert(`${$LL.MODERATOR.WORD_FILTER.EDIT_WORD_FILTER_ERROR()}: ${result['title']}`);
        }

    }
</script>

{#if check_permission(user_info, permissions.manage_word_filter)}
    <Section header={$LL.MODERATOR.WORD_FILTER.WORD_FILTER_LIST()}>
        <div>
            {$LL.MODERATOR.WORD_FILTER.BLACKLISTED_WORDS()}
        </div>
        <div>
            <textarea bind:value={words_text}/>
        </div>
        <div>
            <Button on:click={editFilter}>{$LL.COMMON.SAVE()}</Button>
        </div>
    </Section>
{:else}
    {$LL.COMMON.NO_PERMISSION()}
{/if}


<style>
    textarea {
        width: 100%;
        min-height: 500px;
    }
</style>