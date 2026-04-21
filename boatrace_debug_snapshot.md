# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-04-21T15:40:02.036068+09:00

### 次に取るべきアクション
> RED最優先: ⚠️ DB更新が9分前（run_cycle停止疑い・今レース時間帯） → ログ/DB確認

### 検出された問題
- 🔴 ⚠️ DB更新が9分前（run_cycle停止疑い・今レース時間帯）

---

以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `657711d6153ff6f442c9436df8dd5201`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 1.09MB / last modified 2026-04-21T15:31:21.421924+09:00

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
```

### 直近 run_cycle ログ (末尾)
```
ombos: {'win': 6, '2t': 29, '3t': 120}
2026-04-21 15:39:20,170 [INFO] run_cycle: fetched 13/11 [final]: 155 combos
2026-04-21 15:39:23,782 [INFO] scraper: odds3t: 120/120 parsed
2026-04-21 15:39:24,887 [INFO] scraper: odds3f: 20/20 parsed
2026-04-21 15:39:25,994 [INFO] scraper: odds2t: 30/30 parsed
2026-04-21 15:39:25,995 [INFO] scraper: odds2f: 15/15 parsed
2026-04-21 15:39:27,150 [INFO] scraper: odds_win: 5/6 parsed
2026-04-21 15:39:27,150 [INFO] scraper: fetch_race 01/2: boats=6 odds=190/191
2026-04-21 15:39:27,157 [INFO] predictor: CALIBRATION_MODE=on
2026-04-21 15:39:27,157 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-04-21 15:39:27,165 [INFO] run_cycle: fetched 01/2 [scan]: 155 combos
2026-04-21 15:39:30,920 [INFO] scraper: odds3t: 120/120 parsed
2026-04-21 15:39:32,074 [INFO] scraper: odds3f: 20/20 parsed
2026-04-21 15:39:33,166 [INFO] scraper: odds2t: 30/30 parsed
2026-04-21 15:39:33,167 [INFO] scraper: odds2f: 15/15 parsed
2026-04-21 15:39:34,235 [INFO] scraper: odds_win: 3/6 parsed
2026-04-21 15:39:34,235 [INFO] scraper: fetch_race 11/11: boats=6 odds=188/191
2026-04-21 15:39:34,244 [INFO] predictor: CALIBRATION_MODE=on
2026-04-21 15:39:34,246 [INFO] predictor: combos: {'win': 3, '2t': 30, '3t': 120}
2026-04-21 15:39:34,252 [INFO] run_cycle: fetched 11/11 [scan]: 153 combos
2026-04-21 15:39:37,759 [INFO] scraper: odds3t: 120/120 parsed
2026-04-21 15:39:38,922 [INFO] scraper: odds3f: 20/20 parsed
2026-04-21 15:39:40,067 [INFO] scraper: odds2t: 30/30 parsed
2026-04-21 15:39:40,068 [INFO] scraper: odds2f: 12/15 parsed
2026-04-21 15:39:41,181 [INFO] scraper: odds_win: 2/6 parsed
2026-04-21 15:39:41,181 [INFO] scraper: fetch_race 07/2: boats=6 odds=184/191
2026-04-21 15:39:41,193 [INFO] predictor: CALIBRATION_MODE=on
2026-04-21 15:39:41,193 [INFO] predictor: combos: {'win': 2, '2t': 30, '3t': 120}
2026-04-21 15:39:41,201 [INFO] run_cycle: fetched 07/2 [scan]: 152 combos
2026-04-21 15:39:41,396 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 20
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 20
  }
]
```

## Phase別通知記録 (24h)
{'final': 6, 'result': 10, 'scan': 4}

## アラート件数 (24h・種類別)
```
  (なし)
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 10 | 1 | 3,000 | 1,140 | -1,860 | 0.38 |

## 直近アラート (24h・新しい順)
```
[23:59:06] FINAL_MISSING: {"kind": "FINAL_MISSING", "nid": "2026042022051425", "sid": "S00", "deadline": "2026-04-20T14:25:00+09:00"}
```

## 本日残レース: 62件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 94件 締切済
- 通知発射: scan=3 nid / final=4 nid / result=4 nid
- predictions: 4 / うち結果DB記録済: 4
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 225R | win | 1 | 0.5719 | 8.5 | 4.86 | 300 | scan=7.5 drift=+13.3% | 14:22:21 |
| S00 | 056R | win | 1 | 0.5035 | 6.5 | 3.27 | 300 | scan=6.6 drift=-1.5% | 13:58:20 |
| S00 | 186R | win | 1 | 0.5057 | 7.0 | 3.54 | 300 | scan=- drift=- | 10:45:20 |
| S00 | 185R | win | 1 | 0.4694 | 4.0 | 1.88 | 300 | scan=- drift=- | 10:15:20 |
| S00 | 073R | win | 1 | 0.5477 | 5.1 | 2.79 | 300 | scan=- drift=- | 16:09:21 |
| S00 | 223R | win | 1 | 0.3561 | 41.2 | 14.67 | 300 | scan=36.7 drift=+12.3% | 13:26:31 |
| S00 | 187R | win | 1 | 0.1608 | 6.9 | 1.11 | 300 | scan=5.3 drift=+30.2% | 11:25:20 |
| S00 | 186R | win | 1 | 0.5364 | 5.1 | 2.74 | 300 | scan=- drift=- | 10:53:20 |
| S00 | 094R | win | 1 | 0.4781 | 9.0 | 4.30 | 300 | scan=- drift=- | 12:07:21 |
| S00 | 092R | win | 1 | 0.4219 | 7.7 | 3.25 | 300 | scan=- drift=- | 11:05:20 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 4 | +13.6% | -1.5% | +30.2% | 0 | 0 | 3 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 299.9s |
| **Latency** (scan→final max) | 412.6s |
| **Traffic** (notifications 24h) | 20 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 10 | 0.4552 | 0.1000 | +0.3552 | 🔴+78% | 0.2108 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 10 | 0.4552 | 0.1000 | 0.2108 | 🔴-1.34 | 0.38 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.50+ | 5 | 0.5330 | 0.2000 | 🔴+0.3330 |

## Settlement Ratio データ品質

- 学習済み: 0バンド / fallback: 16バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ⚠️fallback | 0 | 0.4 |
| win | <5.0 | ⚠️fallback | 0 | 0.35 |
| win | <10.0 | ⚠️fallback | 1 | 0.32 |
| win | <20.0 | ⚠️fallback | 0 | 0.22 |
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
_auto-generated by claude_snapshot.py at 2026-04-21T15:40:02.036068+09:00_