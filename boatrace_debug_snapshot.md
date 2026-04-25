# ClaudeDebug スナップショット

## 🟡 現状: YELLOW

**生成**: 2026-04-26T05:30:02.095896+09:00

### 次に取るべきアクション
> YELLOW監視: FINAL_MISSING×106 (24h)

### 検出された問題
- 🟡 FINAL_MISSING×106 (24h)

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×17  [2026-04-25T16:44:41]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_BET_VOLUME_SPIKE  ×14  [2026-04-25T12:45:48]
- key: `ANOMALY_BET_VOLUME_SPIKE|`
- **FIX**: 本日のbet数が2σ急増。filter logic緩み・戦略追加・race_schedule異常

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×39  [2026-04-25T11:40:35]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×15  [2026-04-25T10:00:25]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ ROI_STAT  ×1  [2026-04-25T06:00:07]
- key: `ROI_STAT|S00: n=36 hit%=25.0% hit_CI[Bonf]=[10.3,49.1]% ROI=0.94 ROI_boot95=[0.41,1.56]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-04-25T06:00:07]
- key: `INSUFFICIENT_SAMPLE|S00: n=36<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-04-25T06:00:07]
- key: `ORPHAN_SCAN|28 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ CALIBRATION_LIVE  ×1  [2026-04-25T06:00:07]
- key: `CALIBRATION_LIVE|bt=win: n=36 pred=0.4350 actual=0.2500 error=+0.1850 (+43%) brier=0.2324 [OVERCO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-04-25T06:00:07]
- key: `CALIBRATION_LIVE|S00(win): n=36 pred=0.4350 hit=0.2500 cal_err=+0.1850 brier=0.2324 BSS=-0.24 ROI`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-04-25T06:00:07]
- key: `CALIBRATION_LIVE|decile 0.40-0.50: n=14 pred=0.4396 actual=0.2143 gap=+0.2254`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-04-25T06:00:07]
- key: `CALIBRATION_LIVE|decile 0.50+: n=16 pred=0.5271 actual=0.3125 gap=+0.2146`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-04-25T06:00:07]
- key: `PAYOUT_RATIO_WEIRD|pid=759 bet=300 odds=4.0 payout=1980 ratio=1.65`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-04-25T06:00:07]
- key: `PAYOUT_RATIO_WEIRD|pid=881 bet=300 odds=12.7 payout=900 ratio=0.24`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `149bfa9ecc7e714a646f5a33d43fea95`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 1.21MB / last modified 2026-04-26T05:30:02.597817+09:00

### データファイル存在確認
| file | exists | md5 | size |
|---|---|---|---|
| lgbm_model_top1.txt | True | `5b55d55bdb59df95ccfd1745d4e9b469` | 769682 |
| lgbm_model_top3.txt | True | `d5fd8d8393fd859ed913813abbf60084` | 969111 |
| calibration_v7.json | True | `1c04ab3c1a1f074da889e6f5f06adbf3` | 1450 |
| pl_corr_v8_final.json | True | `8727224dfcc3d7548845e2e41caef7be` | 1209 |

### crontab
```
# boatrace_v2 - managed by めう/Claude
SHELL=/bin/bash
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

# 1分毎: 統合サイクル (run_cycle.py, flock で並行実行防止)
* 8-23 * * * cd /opt/boatrace_v2 && flock -n /var/lock/run_cycle.lock /opt/boatrace/venv/bin/python3 run_cycle.py >> logs/run_cycle.log 2>&1

# 10分毎: pending alert flush
*/10 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 dispatch_pending.py >> logs/dispatch.log 2>&1

# 10分毎: snapshot 生成 + GitHub 同期 (Claude 次セッション用)
*/10 * * * * cd /opt/boatrace_v2 && bash sync_snapshot_to_github.sh >> logs/sync_snapshot.log 2>&1

# 5分毎: 結果取得
*/5 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 record_results.py >> logs/results.log 2>&1

# 30分毎: health check
*/30 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 health.py >> logs/health.log 2>&1

# 6時: 日次総合検査
0 6 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 verify_all.py >> logs/verify_all.log 2>&1

# 0時: 日次集計
5 0 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 daily_summary.py >> logs/daily.log 2>&1
0 3 * * * find /opt -maxdepth 1 -name "boatrace_v2.bak_*" -mtime +7 -exec rm -rf {} \; # backup cleanup

# 30分毎: コード/DB a
```

### 直近 run_cycle ログ (末尾)
```
49 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-04-25 23:55:06,149 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-04-25 23:55:06,219 [INFO] predictor: Models loaded OK
2026-04-25 23:55:06,226 [INFO] run_cycle: run_cycle done: 0 notifications
2026-04-25 23:56:05,512 [INFO] run_cycle: === run_cycle 23:56:05 ===
2026-04-25 23:56:05,512 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-04-25 23:56:05,512 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-04-25 23:56:05,558 [INFO] predictor: Models loaded OK
2026-04-25 23:56:05,563 [INFO] run_cycle: run_cycle done: 0 notifications
2026-04-25 23:57:05,692 [INFO] run_cycle: === run_cycle 23:57:05 ===
2026-04-25 23:57:05,692 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-04-25 23:57:05,692 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-04-25 23:57:05,756 [INFO] predictor: Models loaded OK
2026-04-25 23:57:05,763 [INFO] run_cycle: run_cycle done: 0 notifications
2026-04-25 23:58:06,170 [INFO] run_cycle: === run_cycle 23:58:06 ===
2026-04-25 23:58:06,170 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-04-25 23:58:06,170 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-04-25 23:58:06,220 [INFO] predictor: Models loaded OK
2026-04-25 23:58:06,225 [INFO] run_cycle: run_cycle done: 0 notifications
2026-04-25 23:59:05,609 [INFO] run_cycle: === run_cycle 23:59:05 ===
2026-04-25 23:59:05,609 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-04-25 23:59:05,609 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-04-25 23:59:05,680 [INFO] predictor: Models loaded OK
2026-04-25 23:59:05,686 [INFO] run_cycle: run_cycle done: 0 notifications

```

## 戦略有効/無効一覧
| id | trust | bt | ev_th | pmin | enabled |
|---|---|---|---|---|---|
| S00 | S | win | 4.0 | 0.0 | True |

## Webhook送信 (24h)
```
[
  {
    "target": "mirror",
    "ok": 1,
    "c": 47
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 47
  }
]
```

## Phase別通知記録 (24h)
{'final': 15, 'result': 11, 'scan': 21}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 150
  FINAL_MISSING: 106
  ANOMALY_SCAN_FINAL_RATIO: 3
  ANOMALY_BET_VOLUME_DROP: 1
  ANOMALY_BET_VOLUME_SPIKE: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 45 | 12 | 13,500 | 13,830 | +330 | 1.024 |

## 直近アラート (24h・新しい順)
```
[23:58:06] FINAL_MISSING: {"deadline": "2026-04-25T13:22:00+09:00", "kind": "FINAL_MISSING", "nid": "2026042504061322", "sid": "S00"}
[23:53:05] FINAL_MISSING: {"deadline": "2026-04-25T11:16:00+09:00", "kind": "FINAL_MISSING", "nid": "2026042508031116", "sid": "S00"}
[23:46:06] FINAL_MISSING: {"deadline": "2026-04-25T15:10:00+09:00", "kind": "FINAL_MISSING", "nid": "2026042506081510", "sid": "S00"}
[23:34:06] FINAL_MISSING: {"deadline": "2026-04-25T13:57:00+09:00", "kind": "FINAL_MISSING", "nid": "2026042522041357", "sid": "S00"}
[23:31:05] FINAL_MISSING: {"deadline": "2026-04-25T11:53:00+09:00", "kind": "FINAL_MISSING", "nid": "2026042504031153", "sid": "S00"}
[23:29:06] FINAL_MISSING: {"deadline": "2026-04-25T11:49:00+09:00", "kind": "FINAL_MISSING", "nid": "2026042516031149", "sid": "S00"}
[23:19:06] FINAL_MISSING: {"deadline": "2026-04-25T17:47:00+09:00", "kind": "FINAL_MISSING", "nid": "2026042515061747", "sid": "S00"}
[23:13:05] FINAL_MISSING: {"deadline": "2026-04-25T18:40:00+09:00", "kind": "FINAL_MISSING", "nid": "2026042512081840", "sid": "S00"}
[23:10:08] FINAL_MISSING: {"deadline": "2026-04-25T16:38:00+09:00", "kind": "FINAL_MISSING", "nid": "2026042520041638", "sid": "S00"}
[23:07:06] FINAL_MISSING: {"deadline": "2026-04-25T10:29:00+09:00", "kind": "FINAL_MISSING", "nid": "2026042509011029", "sid": "S00"}
```

## 本日残レース: 0件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 0件 登録 / 0件 締切済
- 通知発射: scan=0 nid / final=0 nid / result=0 nid
- predictions: 0 / うち結果DB記録済: 0
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 206R | win | 1 | 0.5990 | 5.7 | 3.41 | 300 | scan=- drift=- | 17:29:20 |
| S00 | 153R | win | 1 | 0.4111 | 4.6 | 1.89 | 300 | scan=6.0 drift=-23.3% | 16:21:44 |
| S00 | 152R | win | 1 | 0.5123 | 17.2 | 8.81 | 300 | scan=6.7 drift=+156.7% | 15:49:29 |
| S00 | 223R | win | 1 | 0.5891 | 4.3 | 2.53 | 300 | scan=- drift=- | 13:28:21 |
| S00 | 086R | win | 1 | 0.4989 | 8.4 | 4.19 | 300 | scan=4.7 drift=+78.7% | 12:45:33 |
| S00 | 239R | win | 1 | 0.4111 | 4.0 | 1.64 | 300 | scan=- drift=- | 12:20:43 |
| S00 | 044R | win | 1 | 0.0920 | 10.2 | 0.94 | 300 | scan=20.0 drift=-49.0% | 12:20:35 |
| S00 | 164R | win | 1 | 0.1957 | 7.2 | 1.41 | 300 | scan=- drift=- | 12:16:22 |
| S00 | 093R | win | 1 | 0.4989 | 14.2 | 7.08 | 300 | scan=- drift=- | 11:23:20 |
| S00 | 041R | win | 1 | 0.4854 | 6.7 | 3.25 | 300 | scan=8.0 drift=-16.2% | 10:52:21 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 25 | +16.2% | -68.2% | +156.7% | 10 | 5 | 22 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 457.1s |
| **Latency** (scan→final max) | 666.4s |
| **Traffic** (notifications 24h) | 47 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 47 | 0.4333 | 0.2553 | +0.1780 | 🟡+41% | 0.2336 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 47 | 0.4333 | 0.2553 | 0.2336 | 🔴-0.23 | 0.981 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.30-0.50 | 22 | 0.4339 | 0.2727 | 🔴+0.1612 |
| 0.50+ | 19 | 0.5334 | 0.2632 | 🔴+0.2702 |

## Settlement Ratio データ品質

- 学習済み: 0バンド / fallback: 16バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ⚠️fallback | 0 | 0.4 |
| win | <5.0 | ⚠️fallback | 3 | 0.35 |
| win | <10.0 | ⚠️fallback | 7 | 0.32 |
| win | <20.0 | ⚠️fallback | 2 | 0.22 |
| win | <50.0 | ⚠️fallback | 0 | 0.1 |
| win | ∞ | ⚠️fallback | 0 | 0.1 |
| 2t | <10.0 | ⚠️fallback | 0 | 0.5 |
| 2t | <30.0 | ⚠️fallback | 0 | 0.35 |
| 2t | ∞ | ⚠️fallback | 0 | 0.25 |
| 3t | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3t | <200.0 | ⚠️fallback | 0 | 0.3 |
| 3t | ∞ | ⚠️fallback | 0 | 0.2 |
| 2f | <10.0 | ⚠️fallback | 0 | 0.45 |
| 2f | ∞ | ⚠️fallback | 0 | 0.3 |
| 3f | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3f | ∞ | ⚠️fallback | 0 | 0.25 |

---
_auto-generated by claude_snapshot.py at 2026-04-26T05:30:02.095896+09:00_