# WOD5e Impairment

A Foundry VTT module for the World of Darkness 5th Edition system (wod5e). Adds automatic impairment penalties and optional crippling injuries mechanics.

## Requirements

- Foundry VTT v13+
- [wod5e](https://github.com/WoD5E-Developers/wod5e) system
- [libWrapper](https://foundryvtt.com/packages/lib-wrapper) module

## Features

### Automatic Impairment

Works out of the box with no configuration needed.

- **Health Impairment**: When all health boxes are filled with damage (superficial + aggravated), a -2 penalty is automatically applied to all Physical rolls. Werewolves in Crinos form have their bonus health pool taken into account. Does not apply during Frenzy.
- **Willpower Impairment**: When all willpower boxes are filled with damage, a -2 penalty is automatically applied to all Social and Mental rolls.

These penalties appear as modifiers on the character sheet and are applied to dice rolls automatically.

### Crippling Injuries (Optional)

Disabled by default. Must be configured in module settings.

When a character's health tracker is completely filled with damage, additional damage may cause a crippling injury. This module implements the Crippling Injury table:

| Roll (d10 + Aggravated) | Injury | Effect |
|---|---|---|
| 1-6 | Stunned | Spend 1 Willpower or lose a turn |
| 7-8 | Severe Head Trauma | Physical rolls at -1; Mental rolls at -2 |
| 9-10 | Broken Limb / Blinded | -3 to rolls using affected limb, or -3 to vision/combat rolls |
| 11 | Massive Wound | All rolls at -2; +1 to all additional damage |
| 12 | Crippled | Limb lost or mangled; -3 to rolls using affected limb |
| 13+ | Death | Fatal wound |

#### Configuration

1. Go to **Module Settings** > **WOD5e Impairment** > click **Configure** next to "Crippling Injuries"
2. A table appears with three columns: **PC**, **NPC**, and **No Heal**
3. **PC / NPC**: Check the boxes for each injury type you want to enable, separately for player characters and NPCs
4. **No Heal**: Check this box to prevent the Heal Injury button from removing this condition. Injuries marked No Heal must be removed manually by the Storyteller from the Conditions tab. By default, only "Crippled" has No Heal checked.
5. Use the checkboxes in the column headers to toggle all entries in that column at once
6. Click **Save**

All injury types are disabled by default.

#### Roll Injury

A bone-break icon button appears above the health bar when:
- At least one injury type is enabled for this actor's category (PC or NPC)
- The character's health tracker is completely filled with damage

Clicking the button:
1. Rolls 1d10 and adds the character's current aggravated health damage
2. Posts the full roll breakdown to chat: `(d10: X)+(Aggravated: +Y)= Z`
3. Looks up the result on the injury table (skipping disabled injury types by bumping up to the next enabled one)
4. Applies the effect:
   - **Stunned**: A dialog appears asking the player to spend 1 Willpower or lose their turn.
   - **Severe Head Trauma / Broken Limb / Massive Wound / Crippled**: A condition is created on the character with the appropriate dice penalties. These penalties apply automatically to all future rolls.
   - **Broken Limb / Blinded** (9-10): The condition is created with a -3 physical penalty. The player decides per-roll whether it applies.
   - **Death**: Only a chat message is posted. No condition is created.
   - If the rolled result lands on a disabled injury type and no higher type is enabled, a "Lucky! No injuries!" message is posted instead.

#### Heal Injury

A medical icon button appears above the health bar when the character has at least one healable crippling injury condition.

Clicking the button:
1. Removes the crippling injury condition with the **lowest severity** from the character (e.g., Severe Head Trauma is removed before Massive Wound)
2. Posts a recovery message to chat

**Note:** Conditions marked as **No Heal** in the settings (Crippled by default) cannot be removed by the Heal button. They must be removed manually from the character's Conditions tab. The purpose is that such injuries cannot be quickly healed by regeneration — they require an in-game solution, the simplest of which is time. A warning message is shown if only non-healable injuries remain.

---

# WOD5e Impairment (Українською)

Модуль для Foundry VTT для системи World of Darkness 5th Edition (wod5e). Додає автоматичні штрафи за виснаження та опціональну механіку жахливих ран.

## Вимоги

- Foundry VTT v13+
- Система [wod5e](https://github.com/WoD5E-Developers/wod5e)
- Модуль [libWrapper](https://foundryvtt.com/packages/lib-wrapper)

## Можливості

### Автоматичне виснаження

Працює одразу без налаштувань.

- **Виснаження Здоров'я**: Коли всі клітинки здоров'я заповнені пошкодженнями (поверхневі + аґґравовані), автоматично застосовується штраф -2 до всіх Фізичних кидків. Для перевертнів у формі Крінос враховується додатковий запас здоров'я. Не діє під час Шаленства.
- **Виснаження Сили Волі**: Коли всі клітинки сили волі заповнені пошкодженнями, автоматично застосовується штраф -2 до всіх Соціальних та Ментальних кидків.

Ці штрафи відображаються як модифікатори на листі персонажа та автоматично застосовуються до кидків кубиків.

### Жахливі Рани (Опціонально)

Вимкнено за замовчуванням. Потрібно налаштувати в параметрах модуля.

Коли трекер здоров'я персонажа повністю заповнений пошкодженнями, додаткові пошкодження можуть спричинити жахливу рану. Модуль реалізує таблицю Жахливих Ран:

| Кидок (d10 + Аґґравований) | Рана | Ефект |
|---|---|---|
| 1–6 | Оглушення | Витратити 1 Силу Волі або пропустити хід |
| 7–8 | Важка Травма Голови | Фізичні кидки -1; Ментальні кидки -2 |
| 9–10 | Зламана Кінцівка / Осліплення | -3 до кидків з ушкодженою кінцівкою або -3 до зорових/бойових кидків |
| 11 | Масивна Рана | Усі кидки -2; +1 до всієї додаткової шкоди |
| 12 | Покалічення | Кінцівка втрачена; -3 до кидків з ушкодженою кінцівкою |
| 13+ | Смерть | Смертельна рана |

#### Налаштування

1. Перейдіть до **Налаштування модулів** > **WOD5e Impairment** > натисніть **Налаштувати** біля "Жахливі Рани"
2. З'явиться таблиця з трьома колонками: **PC**, **NPC** та **Без зцілення**
3. **PC / NPC**: Позначте галочками типи ран, які хочете увімкнути, окремо для гравців та НПГ
4. **Без зцілення**: Позначте цю галочку, щоб кнопка Зцілення не могла видалити цей стан. Такі рани потрібно видаляти вручну з вкладки Стани. За замовчуванням позначено лише "Покалічення".
5. Використовуйте галочки у заголовках колонок, щоб увімкнути/вимкнути всі пункти в колонці одразу
6. Натисніть **Save**

Усі типи ран вимкнені за замовчуванням.

#### Кинути Каліцтво

Кнопка з іконкою зламаної кістки з'являється над смужкою здоров'я, коли:
- Хоча б один тип рани увімкнений для категорії цього актора (ПГ або НІП)
- Трекер здоров'я персонажа повністю заповнений пошкодженнями

Натискання кнопки:
1. Кидає 1d10 та додає поточні аґґравовані пошкодження здоров'я персонажа
2. Публікує повний розклад кидка в чат: `(d10: X)+(Аґґравований: +Y)= Z`
3. Шукає результат у таблиці ран (пропускаючи вимкнені типи, переходячи до наступного увімкненого)
4. Застосовує ефект:
   - **Оглушення**: З'являється діалог з вибором — витратити 1 Силу Волі або пропустити хід. Якщо трекер сили волі вже заповнений, витрата перетворює поверхневу клітинку на аґґравовану.
   - **Важка Травма Голови / Зламана Кінцівка / Масивна Рана / Покалічення**: На персонажа створюється стан з відповідними штрафами до кидків. Ці штрафи автоматично застосовуються до всіх подальших кидків.
   - **Зламана Кінцівка / Осліплення** (9–10): Стан створюється зі штрафом -3 до фізичних кидків. Оскільки гравець вирішує для кожного кидка, чи застосовується він, використовуйте **перемикач придушення** на стані у вкладці Стани персонажа для кидків, на які він не впливає.
   - **Смерть**: Публікується лише повідомлення в чат. Стан не створюється.
   - Якщо результат кидка потрапляє на вимкнений тип рани і вищого увімкненого типу немає — публікується повідомлення "Пощастило! Жодних ран!"

#### Зцілити Каліцтво

Кнопка з медичною іконкою з'являється над смужкою здоров'я, коли персонаж має хоча б один стан жахливої рани, що піддається зціленню.

Натискання кнопки:
1. Видаляє стан жахливої рани з **найнижчою тяжкістю** з персонажа (наприклад, Важка Травма Голови видаляється раніше за Масивну Рану)
2. Публікує повідомлення про одужання в чат

**Примітка:** Стани, позначені як **Без зцілення** в налаштуваннях (за замовчуванням — Покалічення), не можуть бути видалені кнопкою Зцілення. Їх потрібно видалити вручну з вкладки Стани персонажа. Такі рани не піддаються швидкому зціленню регенерацією — вони потребують ігрового рішення, найпростіше з яких — час. Якщо залишилися лише незцілювані рани, з'явиться попередження.

<p>Dark Pack</p>
<p><img src="https://images.ctfassets.net/u73tyf0fa8v1/3oBTHBZk9XmfcBlUPylvFh/673e4a6b14566548c03424ddf627b944/darkpack_logo2.png?w=3840&amp;q=75" alt="darkpack_logo2" width="300" height="308" /></p>
<p class="body">&ldquo;Portions of the materials are the copyrights and trademarks of Paradox Interactive AB, and are used with permission. All rights reserved. For more information please visit <a href="http://worldofdarkness.com" target="_blank" rel="nofollow noopener">worldofdarkness.com</a>.&rdquo;</p>
<ul>
<li>
<p class="body">You may not remove or alter any copyright or trademark notices of World of Darkness.</p>
</li>
<li>
<p class="body">Your use of World of Darkness IP is strictly for non-commercial purposes only. For example, you may not offer goods or services for sale in connection with your use of the World of Darkness IP.</p>
</li>
<li>
<p class="body">You may not sell or charge any fees in connection with Your Material, with these exceptions:</p>
</li>
<li>
<p class="body">You may accept donations for your time and materials through Patreon or similar services, or through sponsorships.</p>
</li>
<li>
<p class="body">You may accept subscription fees and revenues allowable through streaming platforms such as Twitch, YouTube, Mixer, etc.</p>
</li>
<li>
<p class="body">You may sell your Material through the Storytellers Vault, our official program that allows you to create and sell certain types of content through our authorized web portal.</p>
</li>
<li>
<p class="body">You warrant and represent that Your Material at all times shall comply with all applicable laws, and that it does not infringe any third party&rsquo;s intellectual property rights or any other right.</p>
</li>
</ul>
