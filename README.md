# AIR audit anchors（監査アンカー・ハッシュのみ）

このリポジトリは [AIR](https://github.com/hironori-oi)（AI 組織の自律経営基盤）の監査ログの
**ハッシュ連鎖ルートだけ**を公開するアンカーです。監査の本文・数値・組織名は含まれません。

- `anchors.jsonl` … 1 行 = 1 アンカー `{ts, root, orgs: {<不透明な組織ID>: {lines, head}}}`
  - 組織IDはローカルで採番した不透明な乱数です。対応表は所有者が監査人へ選択開示できます。
  - `lines`（チェーン行数）は活動量というメタデータであり、ここから組織の稼働規模は推測できます
    ——それを承知で公開しています（隠れて公開しない）。
- 検証: AIR 本体で `python scripts/audit_verify.py`（このリポジトリの記録を正本として照合）

## 何が証明できるか
各アンカー時点より**前**の監査行を後から編集・削除・挿入すると、再計算したチェーンが
ここに公開済みの `head` と一致しなくなります。

## 何が証明できないか（誠実に書く）
- アンカー**以後**に追記された行と、チェーン開始（CHAIN-GENESIS）**以前**に封印された区間の
  行単位の真正性。
- 所有者がアンカー発行を**止めた期間**の改竄。アンカーは周期発行（自律実行の終了時＋手動）です。
- コミットの author 時刻は自己申告です。第三者性の実体は (a) GitHub が push を受領した事実と
  (b) あれば OpenTimestamps の刻印で、このリポジトリ自体も所有者が force-push / 削除できます
  （第三者のクローン・フォーク・OTS がその対策になります）。

Hash-only anchors for AIR's audit logs. Org names are replaced by opaque local IDs;
line counts (activity volume) are intentionally visible. Tampering with any audit line
**before** an anchor breaks verification; limitations above are disclosed honestly.
