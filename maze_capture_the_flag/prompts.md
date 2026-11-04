# Project: Maze Capture the Flag

> - **Files:** maze_capture_the_flag.html (English), maze_capture_the_flag_vi.html (original Vietnamese)
> - **Dates:** 2026-10-25 → 2026-11-04
> - **Defaults:** Claude · Sonnet 5.5
> - **Status:** prototype
> - **Use:** Built as a candidate for a ChatGPT multiplayer game challenge (due 2026-10-31); not used in any event yet
> - **Reusability:** artifact medium · prompt pattern medium
> - **Tags:** single-file-html, game, canvas, source-material
> - **Takeaway:** One long, very specific design prompt (rules, controls, scoring) produced a playable single-file game; the earlier rounds of trying other game types were what made the prompt specific.
> - **Story value:** anecdote
> - **Surprises:** The assistant found a real fairness bug (the bot had rules the player's side lacked) by running 30 automated bot-vs-bot matches. Earlier versions (territory capture, dice duel) were scrapped because they felt "clunky and hard to play".

Background: this is a single-player preview of a two-team capture-the-flag game. I play BLUE against a RED bot. The 12 pixel-art zodiac characters were made earlier for my Astraeum Tower dungeon game. The full online multiplayer version was meant to be built in ChatGPT, so this prototype was for working out the rules.

# Prompt 1 (maze capture-the-flag redesign, written in Vietnamese):

> - **Tool:** Claude · Sonnet 5.5 · 2026-10-26
> - **Session:** continued · attached: none
> - **Verified:** agent-tested
> - **Human edits:** none

rút thời gian còn 5 phút, lệnh còn tấn công và phòng thủ, map là kiểu giống trong astraeum di chuyển theo bố cục và chướng ngại (như ko thể xuyên tường, làm kiểu dungeon mê cung nhiều ngõ ngách nhưng vẫn phân ra các phòng có thể chọn để làm căn cứ, các phòng ko được chọn thì ko có tác dụng gì ngoài căn phòng bình thường, random vật phẩm hoặc rương mỗi lần cho tất cả các phòng) và có thể chọn 1 nhân vật cố định đầu trận để làm thủ lĩnh, có thể điều khiển thủ lĩnh dò đường trong mê cung để tìm vật phẩm (có thể hồi máu hoặc tăng tấn công/phòng thủ tuỳ loại) và dẫn dắt 6 đội viên đi theo để cùng tấn công. 5 nhân vật còn lại sẽ ở lại để canh giữ cờ, cũng sẽ chọn 1 thủ lĩnh của team phòng thủ để đổi qua điều khiển khi cần. 2 bên sẽ dò đường và lụm rương/ vật phẩm trong lúc tìm phòng chứa cờ của đối thủ để cướp. cách tính điểm giữ nguyên. thêm nút tương tác để thủ lĩnh cướp cờ hoặc lấy lại cờ. trên đường mang cờ về vẫn có thể chiến đấu để giành lại. các nút điều khiển sẽ bao gồm di chuyển 4 hướng, đổi thủ lĩnh để quan sát chỉ đạo 2 team phòng thủ hoặc tất công, tương tác để nhặt cờ, rút lui (khi muốn ổn định lại đội hình team), tấn công (khi đối đầu với team địch). các thủ lĩnh khi ko trong mode bị điều khiển thì vẫn auto làm theo vai trò chung, lúc chọn nút tấn công thì auto đánh như những nhân vật còn lại. các nhân vật sẽ đánh thường 1 lần rồi xài skill nguyên tố (có hồi chiêu 3s).

(English gist, added for the repo: shorten the match to 5 minutes; keep only Attack and Defend orders; make the map a dungeon maze with real walls and selectable rooms; pick a fixed leader to steer through the maze while 6 followers tag along; 5 other characters guard the flag with their own leader; add an Interact button to steal or recover the flag; fighting continues while carrying the flag; controls are 4-way movement, switch leader, interact, retreat and attack; leaders not being steered follow their role automatically; characters use a basic hit and then an elemental skill on a 3s cooldown.)

## Output 1:

(The final message from this turn was copied from my chat history. I could only retrieve its middle and end, so the opening paragraph is missing here. Original text, in Vietnamese.)

**Cách chơi**
- **Mê cung:** 31x13 ô, có tường thật, tạo ngẫu nhiên mỗi trận. Có 11 phòng, đối xứng hai bên để công bằng. Đường đi bị chặn, có ngõ ngách và vòng lặp.
- **Chọn thủ lĩnh Tấn công:** dẫn 6 đội viên đi theo thành hàng. Bạn điều khiển nó bằng ▲◀▶▼ (hoặc WASD, mũi tên).
- **Chọn thủ lĩnh Phòng thủ:** canh cờ cùng 4 người, tự đánh khi địch đến. Bấm "Đổi thủ lĩnh" (Q) để chuyển sang điều khiển nó, và thủ lĩnh kia chuyển sang tự chạy.
- **Chọn phòng làm căn cứ:** cờ và đội giữ cờ ở đó, phòng không chọn chỉ là phòng thường. Căn cứ bot được chọn xa căn cứ bạn.
- **Rương và vật phẩm:** mỗi phòng có 1 vật phẩm (hồi máu, tăng tấn công hoặc tăng phòng thủ cho cả đội người nhặt). Cũng có rương mở ra ngẫu nhiên một trong ba loại.
- **Sương mù:** bạn thấy cả sơ đồ mê cung nhưng chỉ thấy địch, cờ và vật phẩm trong tầm nhìn.
- **Nút bấm:**
  - **Tương tác (E):** nhặt cờ địch, hoặc lấy lại cờ nhà.
  - **Rút lui (R):** đội dừng đánh và về đội hình, chạy nhanh hơn trong 4 giây.
  - **Tấn công (F):** bật thì thủ lĩnh đang lái cũng tự đánh. Mặc định thủ lĩnh không đánh cho đến khi bạn bấm.
- **Mang cờ về:** thủ lĩnh cầm cờ phải về phòng căn cứ của mình mới ghi điểm. Đi đường vẫn đánh nhau, người mang cờ bị hạ thì cờ rơi xuống đất.
- **Điểm số và thời gian:** giữ nguyên (+10 mỗi lần cướp, mỗi 30 giây +2 nếu cờ nhà an toàn, +1 nếu đang giữ cờ địch), trận 5 phút.
- **Chiến đấu:** đánh thường rồi tới kỹ năng nguyên tố, hồi chiêu 3 giây. Kỹ năng được hiện trên thủ lĩnh, các nhân vật khác chỉ có hiệu ứng để đỡ rối mắt.

**Điều mình thấy khi chạy giả lập**
- Hai đội bot mạnh ngang nhau thường gặp nhau rồi đánh gần như diệt nhau, hoặc hòa 20–20 vì mỗi bên còn 5 người giữ cờ. Người chơi thật sẽ lách được nên khó nói trước.
- Mình đã tăng máu lên 1.7 lần để trận không kết thúc trong 40 giây, và cho bot bên đỏ biết tấn công bằng đội phòng thủ khi hết quân tấn công.
- Số liệu (máu, sát thương, vật phẩm, tầm nhìn, tốc độ) đều là con số tạm.

**Chưa kiểm chứng:** font thật (sandbox không tải được), âm thanh, và bấm bằng điện thoại. Nút hướng đã làm cảm ứng nhưng chưa thử trên máy thật.

Bạn chơi một vài trận rồi cho mình biết chỗ nào đang khó chịu nhất (tốc độ, độ khó của bot, tầm nhìn, hay cách điều khiển), mình chỉnh tiếp. Khi bạn hài lòng thì mình viết brief cho ChatGPT làm bản online, còn khoảng 5 ngày đến hạn 31/10.

# Prompt 2 (translate the game into English):

> - **Tool:** Claude · Sonnet 5.5 · 2026-11-04
> - **Session:** continued · attached: none
> - **Verified:** agent-tested
> - **Human edits:** none

convert to english

## Output 2:

I've translated the whole game into English and sent it again as `astraeum-maze-flag.html`. That covers the menus, the rules screen, in-game messages, skill descriptions, room names and the result screens. The zodiac characters now use their English names (Aries, Taurus and so on), and the title is now "Maze Capture the Flag".

I checked that it loads and runs without errors, and I looked at the lineup screen after shortening two long lines that overlapped the Continue button. I did not play a full match, so some of the longer in-game messages may still look crowded.

This is a separate copy; the original Vietnamese artifact is unchanged.
