# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-04-25T14:10:01.924144+09:00

### 次に取るべきアクション
> RED最優先: CALIBRATION_DRIFT×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×92 (24h)
- 🔴 CALIBRATION_DRIFT×1 (24h)

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×36  [2026-04-25T13:33:41]
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
- DB: 1.2MB / last modified 2026-04-25T14:09:46.257415+09:00

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
&hd=20260425: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-04-25 14:09:28,181 [INFO] scraper: odds3t: 120/120 parsed
2026-04-25 14:09:29,306 [INFO] scraper: odds3f: 20/20 parsed
2026-04-25 14:09:30,461 [INFO] scraper: odds2t: 30/30 parsed
2026-04-25 14:09:30,462 [INFO] scraper: odds2f: 15/15 parsed
2026-04-25 14:09:31,547 [INFO] scraper: odds_win: 6/6 parsed
2026-04-25 14:09:31,547 [INFO] scraper: fetch_race 06/6: boats=6 odds=191/191
2026-04-25 14:09:31,560 [INFO] predictor: CALIBRATION_MODE=on
2026-04-25 14:09:31,560 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-04-25 14:09:31,567 [INFO] run_cycle: fetched 06/6 [final]: 156 combos
2026-04-25 14:09:35,141 [INFO] scraper: odds3t: 120/120 parsed
2026-04-25 14:09:36,283 [INFO] scraper: odds3f: 20/20 parsed
2026-04-25 14:09:37,461 [INFO] scraper: odds2t: 30/30 parsed
2026-04-25 14:09:37,463 [INFO] scraper: odds2f: 15/15 parsed
2026-04-25 14:09:38,592 [INFO] scraper: odds_win: 6/6 parsed
2026-04-25 14:09:38,592 [INFO] scraper: fetch_race 17/8: boats=6 odds=191/191
2026-04-25 14:09:38,601 [INFO] predictor: CALIBRATION_MODE=on
2026-04-25 14:09:38,601 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-04-25 14:09:38,609 [INFO] run_cycle: fetched 17/8 [scan]: 156 combos
2026-04-25 14:09:42,485 [INFO] scraper: odds3t: 120/120 parsed
2026-04-25 14:09:43,602 [INFO] scraper: odds3f: 20/20 parsed
2026-04-25 14:09:44,713 [INFO] scraper: odds2t: 30/30 parsed
2026-04-25 14:09:44,714 [INFO] scraper: odds2f: 14/15 parsed
2026-04-25 14:09:46,108 [INFO] scraper: odds_win: 5/6 parsed
2026-04-25 14:09:46,108 [INFO] scraper: fetch_race 08/9: boats=6 odds=189/191
2026-04-25 14:09:46,117 [INFO] predictor: CALIBRATION_MODE=on
2026-04-25 14:09:46,117 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-04-25 14:09:46,125 [INFO] run_cycle: fetched 08/9 [scan]: 155 combos
2026-04-25 14:09:46,233 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 44
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 44
  }
]
```

## Phase別通知記録 (24h)
{'final': 14, 'result': 13, 'scan': 17}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 194
  FINAL_MISSING: 92
  ANOMALY_SCAN_FINAL_RATIO: 4
  ANOMALY_BET_VOLUME_SPIKE: 3
  ANOMALY_BET_VOLUME_DROP: 1
  CALIBRATION_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 42 | 11 | 12,600 | 11,280 | -1,320 | 0.895 |

## 直近アラート (24h・新しい順)
```
[14:09:46] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1178}
[14:07:06] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1190}
[14:05:32] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1181}
[14:04:28] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1189}
[14:03:29] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1180}
[14:02:06] FINAL_MISSING: {"deadline": "2026-04-25T10:29:00+09:00", "kind": "FINAL_MISSING", "nid": "2026042509011029", "sid": "S00"}
[14:02:06] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1185}
[14:01:19] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1206}
[14:00:33] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1197}
[13:59:06] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1221}
```

## 本日残レース: 105件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 192件 登録 / 87件 締切済
- 通知発射: scan=12 nid / final=10 nid / result=8 nid
- predictions: 8 / うち結果DB記録済: 8
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 6件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 223R | win | 1 | 0.5891 | 4.3 | 2.53 | 300 | scan=- drift=- | 13:28:21 |
| S00 | 086R | win | 1 | 0.4989 | 8.4 | 4.19 | 300 | scan=4.7 drift=+78.7% | 12:45:33 |
| S00 | 239R | win | 1 | 0.4111 | 4.0 | 1.64 | 300 | scan=- drift=- | 12:20:43 |
| S00 | 044R | win | 1 | 0.0920 | 10.2 | 0.94 | 300 | scan=20.0 drift=-49.0% | 12:20:35 |
| S00 | 164R | win | 1 | 0.1957 | 7.2 | 1.41 | 300 | scan=- drift=- | 12:16:22 |
| S00 | 093R | win | 1 | 0.4989 | 14.2 | 7.08 | 300 | scan=- drift=- | 11:23:20 |
| S00 | 041R | win | 1 | 0.4854 | 6.7 | 3.25 | 300 | scan=8.0 drift=-16.2% | 10:52:21 |
| S00 | 235R | win | 1 | 0.4111 | 9.5 | 3.91 | 300 | scan=9.5 drift=+0.0% | 10:15:21 |
| S00 | 078R | win | 1 | 0.5123 | 7.1 | 3.64 | 300 | scan=17.8 drift=-60.1% | 18:36:21 |
| S00 | 1610R | win | 1 | 0.5123 | 5.1 | 2.61 | 300 | scan=- drift=- | 15:34:32 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 23 | +11.8% | -68.2% | +156.7% | 9 | 5 | 20 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 433.6s |
| **Latency** (scan→final max) | 661.1s |
| **Traffic** (notifications 24h) | 44 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 2,400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 44 | 0.4282 | 0.2500 | +0.1782 | 🟡+42% | 0.2275 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 44 | 0.4282 | 0.2500 | 0.2275 | 🔴-0.21 | 0.855 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.30-0.50 | 21 | 0.4350 | 0.2381 | 🔴+0.1969 |
| 0.50+ | 17 | 0.5307 | 0.2941 | 🔴+0.2366 |

## Settlement Ratio データ品質

- 学習済み: 0バンド / fallback: 16バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ⚠️fallback | 0 | 0.4 |
| win | <5.0 | ⚠️fallback | 2 | 0.35 |
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
_auto-generated by claude_snapshot.py at 2026-04-25T14:10:01.924144+09:00_